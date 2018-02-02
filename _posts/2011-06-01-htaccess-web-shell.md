---
layout: post
title: Htaccess Web Shell
date: '2011-06-01T11:43:00.000+02:00'
author: Xavier Garcia
tags:
- web shell
- backdoor
- apache
modified_time: '2011-06-01T11:43:54.733+02:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-8003588480991337992
blogger_orig_url: http://www.shellguardians.com/2011/06/htaccess-web-shell.html
---
Via [Mubix](http://twitter.com/#!/mubix/) I have found this [post](http://www.justanotherhacker.com/2011/05/htaccess-based-attacks.html) that describes a new way to upload a web shell to a server.

This method uploads [.hta ccess](http://httpd.apache.org/docs/current/howto/htaccess.html) files to change how the server behaves. The nice trick here is that the file itself:

* Allows the .htaccess files to be displayed
* Tells Apache that the contents of the [.htaccess](http://httpd.apache.org/docs/current/howto/htaccess.html) files must be interpreted by PHP (the file itse lf will be  executed by the PHP interpreter)
* The last part of the file contains PHP code that will pass commands to the operative system.

As a side note, the author also comments t hat this trick can also be applied to jsp and mod_perl installations.

Some informatio n on [securing file uploads](https://www.owasp.org/index.php/Unrestricted_File_Upload), from [OWASP](https://www.owasp.org/).
