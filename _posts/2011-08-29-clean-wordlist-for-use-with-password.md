---
layout: post
title: Clean a wordlist for use with password cracking tools and rules
date: '2011-08-29T13:38:00.001+02:00'
author: Xavier Garcia
tags:
- clean up
- wordlists
modified_time: '2011-08-29T13:39:33.078+02:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-7445063925835046792
blogger_orig_url: http://www.shellguardians.com/2011/08/clean-wordlist-for-use-with-password.html
---
Via [commandlinefu.com](http://www.commandlinefu.com/commands/view/9129/clean-a-wordlist-for-use-with-password-cracking-tools-and-rules)

This post is just a personal note. I am sure I will need this command in the future to clean up my wordlists :)

```shell
$ cat dirtyfile.txt | awk '{gsub(/[[:punct:]]/,"")}1' | tr A-Z a-z | sed 's/[0-9]*//g' | sed -e 's/ //g' | strings | tr -cs '[:alpha:]' ' ' | sed -e 's/ /\n/g' | tr A-Z a-z | sort -u > cleanfile.txt
```
