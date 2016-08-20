---
id: 1288
title: OpenID on protocol7
date: 2006-08-21T19:41:47+00:00
author: Niklas
layout: post
guid: http://www.protocol7.com/archives/2006/08/21/openid-on-protocol7/
permalink: /archives/2006/08/21/openid-on-protocol7/
tags:
  - Security
  - Weblogging
---
<div class='microid-23cb52761f869b820b125e1102adb92ec2bc8320'>
  <p>
    I spent last night working on <a href="http://openid.net/specs.bml">OpenID</a> support for comments on this blog. If you haven&#8217;t taken a look at OpenID yet, you probably should. OpenID is a truly distributed identification system. By providing a URL, an OpenID consumer can then verify with an OpenID server that you really&nbsp;&#8220;are&#8221; that URL, the server will also provide you with the possibility of deciding which consumers you want to share your identity with. And, with the addition of the <a href="http://www.openidenabled.com/openid/simple-registration-extension">Simple Registration extension</a>, you can also provide personal details (such as your nickname and email) if you so like.
  </p>
  
  <p>
    Since I&#8217;m running WordPress, I started googling for for plugins, finding quite a few different versions. After some messing around, I finally chose <a href="http://singpolyma-tech.blogspot.com/2006/04/openid-for-wordpress.html">the version provided by Stephan Paul Weber</a>, which in turn is based on the work of <a href="http://the-notebook.org/12/01/2006/openid-comments-for-wordpress/">Alexander Nikulin</a>. The changes I&#8217;ve done are miniscular in comparison with the work done by Alexander and Stephan, please give credit where credit is due.
  </p>
  
  <p>
    The plugin provides both a consumer for use with post comments and an OpenID server. However, for the server there are multiple free options around the web which are more fully featured so I choose not to use that part of the plugin. Instead, I&#8217;m using the excellent service over at <a href="http://www.myopenid.com">myopenid.com</a>. Since the server is hardcoded into the plugin, this meant that I had to start hacking away at the source. And while I was at it I also fixed two other issues I had with it: didn&#8217;t work with my anti-spam plugin and most of all, didn&#8217;t support Simple Registration. The latter meant that any comment someone would add would use the OpenID URL for the name, instead of, well, the persons name. Also, it didn&#8217;t support getting the persons email either. No good. It also had some minor bugs that I really needed to fix.
  </p>
  
  <p>
    Two hours later, the plugin now support Simple Registration, so adding a comment will now (granted that your OpenID server support Simple Registration and that you&nbsp;approve of providing this information) automatically retrieve your nickname and email and use those in the comment (of course, email is not actually published on the site).&nbsp;Very simple, very slick. Please try it out and give me feedback on how I can improve it! If your OpenID server does not support Simple Registration, the comment consumer should fall back to your URL. Or, you can still comment by only providing your name, email and site, just like before.
  </p>
  
  <p>
    I won&#8217;t package up and release my version of the plugin just yet since I&#8217;m not that confident in that I&#8217;ve made all the necessary changes. Still, if you would like to play around with it, feel free to <a href="mailto:niklas@protocol7.com">email me</a> or leave a comment on this post and I&#8217;ll be happy to send it to you.
  </p>
  
  <p>
    Next up, see if it&#8217;s possible to convince the <a href="http://getk2.com/">K2</a> developers to <a href="http://code.google.com/p/kaytwo/issues/detail?id=100">include support for the OpenID plugin into the theme</a> like they do for many other plugins. That would be outstanding as it would remove the need for hacking the theme as you have to do today.
  </p>
</div>