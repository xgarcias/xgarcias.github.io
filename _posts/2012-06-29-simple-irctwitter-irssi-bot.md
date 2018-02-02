---
layout: post
title: Simple IRC/Twitter Irssi Bot
date: '2012-06-29T10:24:00.002+02:00'
author: Xavier Garcia
tags:
- irssi
- scripting
- perl
- bots
- twitter
modified_time: '2012-06-29T10:24:31.954+02:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-6842821800907732178
blogger_orig_url: http://www.shellguardians.com/2012/06/simple-irctwitter-irssi-bot.html
---
Yesterday I had some free time and I wanted to play a bit with the [Perl API for Irssi](http://irssi.org/documentation/perl), that is a console IRC client if not \*THE\* client.

I don't like like Perl, but it is always nice to learn something new because I always use Python for scripting, that is my preferred language :)

[The Perl script](http://ghosthunter.googlecode.com/svn/trunk/scripts/twitterbot/twitterbot.pl) is a very basic bot that allows the members of a channel to send twits and also to fetch the timeline.  For being on the safe side, sending twits is only allowed for a list of nicks within an specific channel in order to avoid people sending shit or flooding the public chat.

If you want to play a bit,  the API is focused on signals, that are sent when an event happens (e.g. you receive a message). The events can be hooked, stopped, forwarded, etc.. so it is pretty straightforward. But you have to find the right event and it may be not that easy.

For interacting with Twitter, it uses the module Net::Twitter:Lite and [oAuth](https://dev.twitter.com/docs/auth/oauth) authentication.
