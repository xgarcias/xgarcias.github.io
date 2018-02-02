---
layout: post
title: CAs being owned and the SSL trust model
date: '2011-03-24T09:09:00.002+01:00'
author: Xavier Garcia
tags:
- broken
- compromised
- crl
- ca
modified_time: '2011-03-24T09:34:12.615+01:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-588176432325527976
blogger_orig_url: http://www.shellguardians.com/2011/03/cas-being-owned-and-ssl-trust-model.html
---
I really recommend reading this [post](https://blog.torproject.org/blog/detecting-certificate-authority-compromises-and-web-browser-collusion) from Jacob Appelbaum, if you want to understand the story of the compromised CA.  
  
In a short resume, seems like a CA named _COMODO High Assurance Secure Server CA_ was compromised and the attacker issued valid certificates  with their keys.  
  
I quote Comodo's statement:  
  

> One user account in one RA was compromised.The attacker created himself a new userID (with a new username and password) on the compromised user account.

  
Iit seems that some of the issued certificates where: login.live.com, mail.google.com, www.google.com, login.yahoo.com (3 certificates), login.skype.com and addons.mozilla.org.  
  
So far, with the above commented information, we can discuss how broken is the SSL trust model, since  just one compromised CA can cause a big damage and make possible a MITM attack against a big website like mail.google.com.  
  
But that is not all. It seems that the main browser developers were "silently" issuing patches to blacklist the created certificates until Appelbaum  analyzed the serial numbers, as explained in the post.  
  
Also, the Certificate Revocation Lists (CRL) does not seem to work because the browsers "fail open" by default . It means that the browser will not complain if it cannot check the CRL (the CAs do not seem to help a lot to get things better) and the certificate will be blindly accepted, as explained [here](http://www.imperialviolet.org/2011/03/18/revocation.html).  
  
Finally, Comodo  seems to blame the Iranian government  because the attack came from an Iranian IP address,  but in my opinion it does not mean that the Iranian government is behind.
