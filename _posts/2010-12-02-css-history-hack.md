---
layout: post
title: CSS History Hack
date: '2010-12-02T10:46:00.000+01:00'
author: Xavier Garcia
tags:
- css
- hack
- history
modified_time: '2010-12-02T10:46:52.151+01:00'
blogger_id: tag:blogger.com,1999:blog-8534555958859253862.post-6721672947720549912
blogger_orig_url: http://www.shellguardians.com/2010/12/css-history-hack.html
---
The CSS History Hack  is an attack already explained by [Jeremiah Grossman](http://jeremiahgrossman.blogspot.com/2006/08/i-know-where-youve-been.html) in 2006.  In a nutshell, it is possible to use CSS  and Javascript to know which pages has visited our 'guest' before.  How?  The web browser will change the state of the links already visited by the user.  
  
[Forbes](http://blogs.forbes.com/kashmirhill/2010/11/30/history-sniffing-how-youporn-checks-what-other-porn-sites-youve-visited-and-ad-networks-test-the-quality-of-their-data/) explains that some popular sites like YouPorn are using this technique to know which other porn sites the user has visited before.  
  

> How does it work? It’s based on your browser changing the color of links you’ve already clicked on. A script on the site exploits a Web privacy leak to quickly check and see whether your browser reveals that the links to a host of other porn sites have been assigned the color “purple,” meaning you’ve clicked them before. YouPorn did not respond to an inquiry about why it collects this information, and tries to hide the practice by disguising the script with some easy-to-break cryptography.*

  

> The porn site is not alone in its desire to know what other websites visitors have visited. A group of researchers from the University of California – San Diego trolled through the Web’s most popular sites to see which ones were collecting this information about visitors. They found it on 46 other news, finance, sports, and games sites, reporting their findings in a paper with the intimidating title, “[An Empirical Study of Privacy-Violating Information Flows in JavaScript Web Applications](http://cseweb.ucsd.edu/~d1jang/papers/ccs10.pdf).”

  

> The researchers who wrote the paper identifying this practice call it “history hijacking” or “history sniffing.” Mozilla, the foundation behind Web browser Firefox, calls it the “CSS: visited history bug.” It’s a bug that’s been discussed in developer circles for over a decade. Some browsers have fixed the bug. If you’re surfing using Chrome or Safari, this script doesn’t work. Firefox has fixed it in its newest version (for a long explanation as to how, see [this post on the Mozilla security blog](http://blog.mozilla.com/security/2010/03/31/plugging-the-css-history-leak/).) Internet Explorer, [the most popular browser out there](http://blogs.forbes.com/andreaspiegel/2010/11/16/names-you-need-to-know-in-2011-rockmelt-the-social-browser-google-apple-chrome-internet-explorer/#more-102), is vulnerable to the history sniffing (though you can prevent it by going through the slightly onerous step of activating [InPrivate Browsing](http://www.microsoft.com/windows/internet-explorer/features/safer.aspx), according to a spokesperson. That feature also blocks ad networks’ cookies, reports [Business Insider](http://www.businessinsider.com/how-to-use-internet-explorers-do-not-track-feature-2010-11).)
