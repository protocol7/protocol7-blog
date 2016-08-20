---
id: 1533
title: Even easier WP upgrades
date: 2007-10-27T11:56:25+00:00
author: Niklas
layout: post
guid: http://protocol7.com/archives/2007/10/27/even-easier-wp-upgrades/
permalink: /archives/2007/10/27/even-easier-wp-upgrades/
tags:
  - protocol7
  - Subversion
  - Weblogging
openid_comments:
  - 'a:6:{i:0;s:5:"49960";i:1;s:5:"49961";i:2;s:5:"49962";i:3;s:5:"49963";i:4;s:5:"49982";i:5;s:5:"49983";}'
---
<div class='microid-3da9ea61b2f5bfbebc0a567d588cbf22c0e88a44'>
  <p>
    I just upgraded my WordPress installation (the one used to publish this post) to the latest <a href="http://wordpress.org/development/2007/10/wordpress-231/">2.3.1</a>. Upgrading WP is easy, but boring so this time I decided on putting some additional work into the upgrade by switching to the SVN based install <a href="http://codex.wordpress.org/Installing/Updating_WordPress_with_Subversion">described here</a>. Worked like a charm and future updates should now be as easy as running <code>svn switch</code>. I keep the rest of my site in my private SVN since a few years back. That means I would like to keep my WP customizations (like wp-config.php, plugins and themes) in my own SVN and then interleave their working copies to make up the final site. Haven&#8217;t yet figured out how to best do this. Tried soft linking my custom files into the WP checkout, but that blew up WP.
  </p>
</div>