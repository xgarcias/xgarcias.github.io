---
layout: post
title: SSH public key authentication with security tokens
date: '2016-10-21T14:04:00.001+02:00'
author: Xavier Garcia
tags:
- ssh
- yubikey
- piv
- pkcs11
modified_time: '2016-10-21T14:43:22.437+02:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-7280617176677792820
blogger_orig_url: http://www.shellguardians.com/2016/10/ssh-public-key-authentication-with.html
---
I've been using a Yubikey for two factor authentication with HOTP for a long time but this crypto hardware has many more functionalities, like storing certificates (RSA and ECC keys).

The use I will describe below allows us to do SSH public key authentication while keeping the private key stored in the device at all times. This gives an extra layer of security, because the key cannot be extracted and the device will be locked if the PIN is bruteforced.

Formally speaking,  many of these crypto keys (commonly in the form of a USB device emulating a card reader) support the Personal Identity Verification (PIV) card interface, that allows ECC/RSA sign/decryption operations with the private key stored in the device ( Read the [NIST SP 800-78](http://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-78-4.pdf) document for more information). This hardware interface together with the API [PKSC11](https://en.wikipedia.org/wiki/PKCS_11) will allow programs like ssh to perform cryptographic operations with the certificates stored in the device.

One weak point in this scenario is the vendor trust, particularly when it comes to the random number generator implemented in the hardware, that can potentially create weak and easy to bruteforce certificates, but this can be minimized if we use the normal ssh tools to generate the ssh keys and then we import them into the device. In my case, I have followed this path.

Another downside is that NIST SP 800-78 only defines RSA keys up to 2048 bits. You must take this into consideration because the chip may support bigger keys (e.g. for OpenPGP cards) but the PIV interface is up to 2048 unless NIST updates the standard.

Finally, either PKCS11 or [OpenSC](https://github.com/OpenSC/OpenSC/wiki) (I don't quite remember), do not support ECC keys. You are out of luck in that case.

Preparation
===========

* A crypto device that is NIST SP 800-78 compliant, a Yubikey 4 in my case.
* An RSA key pair created with ssh-keygen(1).
* Install [OpenSC](https://github.com/OpenSC/OpenSC/wiki) in your computer to have the PKCS11 library support and management tools. There are installers available for almost any platform: Windows, OSX, Linux, BSD,etc.

Steps
=====

* Convert the RSA private key into pem format.

  ```shell
  $ openssl rsa -in ./id_rsa -out id_rsa.pem
  ```

* Load the private key into the [slot 9a](https://developers.yubico.com/PIV/Introduction/Certificate_slots.html) in the device. It will ask for the PIN, that you may have changed (look for 'change-pin' and 'change-puk'  in [this document](https://www.yubico.com/wp-content/uploads/2016/05/Yubico_PIV_Tool_Command_Line_Guide_en.pdf)). Notice that I've setup the 'pin-policy' to once and the 'touch-policy' to never, effectively asking the PIN only once when I load the key in the ssh-agent, but you can change the behaviour that fits you best (e.g. force a touch every time you want to login via ssh). 

  ```shell
  $ yubico-piv-tool -a import-key -s 9a --pin-policy=once --touch-policy=never  -i id_rsa.pem
  ```

* Transform the public key to a format that is understood by the device

  ```shell
  $ ssh-keygen -e -f ./id_rsa.pub -m PKCS8 > id_rsa.pub.pkcs8
  ```

* Use the public and private keys (the last one in the device) to generate an SSL selfsigned certificate, to be imported later in the device, with a 10 years expiration date (just in case). It will ask for your PIN again.

  ```shell
  $ yubico-piv-tool -a verify -a selfsign-certificate --valid-days 3650  -s 9a -S "/CN=myname/O=ssh/" -i id_rsa.pub.pkcs8 -o 9a-cert.pem
  ```

* Import the generated certificate.

  ```shell
  $ yubico-piv-tool -a verify -a import-certificate -s 9a -i 9a-cert.pem
  ```

Using the device together with OpenSSH
======================================

In case you don't have the public key (this step is not needed because I generated the key in my PC), you can extract it with the ssh-keygen. You have to search for the pkcs11 shared library, that is /Library/OpenSC/lib/pkcs11/opensc-pkcs11.so in case of OSX.

```shell
$ ssh-keygen -D /Library/OpenSC/lib/pkcs11/opensc-pkcs11.so
  ssh-rsa AAAAB....e1
```

Then you can tell ssh to interact with the device by pointing to this library instead of using a private key stored in your disk, but it is not very convenient because it will always ask for your pin.

```shell
$ ssh -I /Library/OpenSC/lib/pkcs11/opensc-pkcs11.so myserver
 Enter PIN for 'PIV_II (PIV Card Holder pin)':
```

Loading the key in your ssh-agent is more convenient because it will only ask for the PIN once (following the pin-policy=once) and you can be sure nobody will try to abuse it because the device must be present at all times. **_Remember that the private key never leaves the device_**.

```shell
$ ssh-add -s /Library/OpenSC/lib/pkcs11/opensc-pkcs11.so
Enter passphrase for PKCS#11:
Card added: /Library/OpenSC/lib/pkcs11/opensc-pkcs11.so 
```

```shell
 bash-3.2$ ssh-add -l
 2048 SHA256:random_hash_value /Library/OpenSC/lib/pkcs11/opensc-pkcs11.so (RSA)
```

```shell
$ ssh-add -e /Library/OpenSC/lib/pkcs11/opensc-pkcs11.so
Card removed: /Library/OpenSC/lib/pkcs11/opensc-pkcs11.so 
```

```shell
$ ssh-add -l
The agent has no identities.
```
