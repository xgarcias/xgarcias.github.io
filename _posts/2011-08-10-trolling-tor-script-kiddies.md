---
layout: post
title: Trolling the Tor Script Kiddies
date: '2011-08-10T13:16:00.002+02:00'
author: Xavier Garcia
tags:
- script kiddies
- Tor
- attack
- contrameasures
modified_time: '2011-08-10T13:52:51.226+02:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-6634264903329139092
blogger_orig_url: http://www.shellguardians.com/2011/08/trolling-tor-script-kiddies.html
---
Following a tweet made by [insit0r](http://twitter.com/insit0r) about script kiddies abusing Tor to attack web sites and blocking them, I thought we should go a bit further and be evil with them.

My first comment was not to block all the Tor exit nodes, since the attacker will use alternative solutions and we will lose visibility. In my opinion, it is better to flag the connection as it is breaking our policies than just blocking, because the second case will not give us information about the intention and skills of the attackers, but only a connection rejected.

So, it is better to receive a warning that flags a possible illegal activit y and correlate/track  the attacker's movements among our infrastructure.

The above comments explain what it comes to be **passive monitoring and information gathering**, but we could switch to our grey hat and do something a little bit evil with our attackers :)

What about sending some  **countermeasures** to our attacker, taking advantage of our position, given that the attacker is not aware he/she has been discovered?

Following this [talk](http://www.shellguardians.com/2011/08/spanish-offensive-security-talk-by.html) in Spanish presented by  [Roberto Martinez](http://twitter.com/r0bertmart1nez), I thought we could use [Mod Security](http://www.modsecurity.org/) to [inject content](http://www.modsecurity.org/projects/modsecurity/apache/feature_content_injection.html) on the pages when we detect someone is connecting through Tor. This gives us the following possibilities:

* Inject a link that redirects them to our honeypot or, better send them to a [Labyrinth to fool their tools and waste their time](http://www.shellguardians.com/2011/05/fooling-bots-and-web-scanners-with.html).
* [Inject objects](http://www.modsecurity.org/blog/archives/2008/01/content_injecti.html) to de-anonymize the attacker.
* Drop back an exploit (not so ethical :D)?

Note: Searching on Google I found this [directory](http://128.31.0.34:9031/tor/status/all) that lists all the Tor exit nodes. Now we have all the tools to troll the script kiddies that want to attack our website.
