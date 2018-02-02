---
layout: post
title: 'Tshark Fu:  decrypting SSL streams'
date: '2010-10-15T16:20:00.002+02:00'
author: Xavier Garcia
tags:
- ssl
- tshark
- decryption
modified_time: '2010-10-15T16:42:16.326+02:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-4036836521784186429
blogger_orig_url: http://www.shellguardians.com/2010/10/tshark-fu-decrypting-ssl-streams.html
---
Nice article from [Pauldotcom](http://www.pauldotcom.com/) about  [decrypting SSL streams with tshark](http://pauldotcom.com/2010/10/tsharkwireshark-ssl-decryption.html), that is focused on HTTPS servers.  
  
The article is easy to follow and explains the full process as well as the problems they found. The following points were particularly interesting:  
  
**Convert the certificate from PKCS#8 to PKCS#1**  

I understand that the private key must be  in PKCS1  because it is the only format understood by tshark.

  
```
openssl pkcs8 -in private.key -out rsaprivate.key -nocrypt
```

  

This point is particularly confusing... I found the following entry in the [Wireshark mailing list](http://seclists.org/wireshark/2009/Nov/78) that explains this problem.  
  
  
**Tshark output and the HTTP parser**  

The following command decrypts the stream and parses the output with tshark's internal HTTP parser.  

```  
tshark -o "ssl.desegment_ssl_records: TRUE"  \
-o "ssl.desegment_ssl_application_data: TRUE" \
-o "ssl.keys_list:,443,http,rsa_private.key"  \
-o "ssl.debug_file:rsa_private.log" -r all.pcap  \
 -R "(tcp.port eq 443)" -V
```
  
This behavior can be changed  if we want to read the raw data. This is achieved by modifying the flags in the third parameter, so we have _data_ instead of  _http_  

```
-o "ssl.keys_list:,443,data,rsa_private.key"
```
