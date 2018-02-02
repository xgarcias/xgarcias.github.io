---
layout: post
title: JavaScript  obfuscation to the next level
date: '2011-02-02T10:53:00.001+01:00'
author: Xavier Garcia
tags:
- xss
- streetfight
- javascript
modified_time: '2011-02-02T10:54:08.066+01:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-6505307655718990824
blogger_orig_url: http://www.shellguardians.com/2011/02/javascript-obfuscation-to-next-level.html
---
Awesome [JavaScript obfuscation](http://adamcecc.blogspot.com/2011/01/javascript.html). The linked post shows a JavaScript code that pops up an alert.  
  
```javascript
($=[$=[]][(__=!$+$)[_=-~-~-~$]+({}+$)[_/_]+  
($$=($_=!''+$)[_/_]+$_[+$])])()[__[_/_]+__  
[_+~$]+$_[_]+$$(_/_)
```
  
This shows how difficult is to detect a client-side attack and also demonstrates why we must design our networks to detect malicious activity once the defenses fail.  
  
The blog post talks about the following [presentation](https://media.blackhat.com/bh-dc-11/Barnett/BlackHat_DC_2011_Barnett_XSS%20Streetfight-wp.pdf) in [Blackhat DC 2011](http://www.blackhat.com/html/bh-dc-11/bh-dc-11-home.html).
