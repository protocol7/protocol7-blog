---
id: 1653
title: Syncing tweets to WordPress
date: 2010-04-04T16:33:04+00:00
author: Niklas
layout: post
guid: http://protocol7.com/?p=1653
permalink: /archives/2010/04/04/syncing-tweets-to-wordpress/
categories:
  - Uncategorized
tags:
  - backup
  - ownyourdata
  - twitter
  - Wordpress
---
<div class='microid-8170ac61128b59e4a7e5b059b18f5211c19eab3a'>
  <p>
    The way old tweets just go missing worries me. This is <a href="http://twitter.com/protocol7/statuses/55813322">my first tweet</a>, <a href="http://www.google.se/search?q=%22Alright,+will+twitter+be+at+all+useful%22">not available on Google Search</a> (at least not when writing this post). While my average tweet isn&#8217;t of much value, over time it builds into something I want to own and have around forever. And I want Google and the others to index it. As usual, this means I want keep it on my own domain. So, I had to set up some form of sync to my <a href="http://protocol7.com/">protocol.com domain</a>. Since I&#8217;m a <a href="http://wordpress.org/">WordPress</a> fanboy, keeping these in WP made sense to me. Turns out, it was simpler than I expected.
  </p>
  
  <p>
    Getting my tweets distills down to two methods: getting the archive and continuously getting the new ones.
  </p>
  
  <p>
    First, I run <a href="http://www.backupify.com/">backupify</a> to keep a basic backup of my online stuff, among that, my twitter stream. Highly recommended. backupify keeps my entire Twitter history as an Atom feed. Now, WordPress still does not support importing posts from Atom, so I had to convert the feed into RSS 2.0. A simple XSL-T stylesheet (<a href="http://github.com/protocol7/atom2rss">available on my GitHub</a>) took care of that. Please note that the stylesheet is purpose-made for this conversion, if you want a generic Atom to RSS 2.0 stylesheet, you might need to be a bit more strict, especially on the date formatting.
  </p>
  
  <p>
    So, now I had all my tweets as a RSS 2.0 feed. I could start importing this into WordPress. Turns out the import would die after some hundred tweets (perhaps something with my MySQL settings) but since the importer verifies duplicates, I could simple just rerun the job until all entries was imported.
  </p>
  
  <p>
    Then, to get continuos synchronization, I use the <a href="http://wordpress.org/extend/plugins/twitter-tools">Twitter tools plugin for WordPress</a>. It will poll my Twitter stream every 10 minutes and create posts for every new tweet. Works as designed.
  </p>
  
  <p>
    <img src="http://protocol7.com/wp/wp-content/uploads/2010/04/twitter-tools-300x203.png" alt="twitter-tools" title="twitter-tools" width="300" height="203" class="alignright size-medium wp-image-1654" srcset="http://protocol7.com/wp/wp-content/uploads/2010/04/twitter-tools-300x203.png 300w, http://protocol7.com/wp/wp-content/uploads/2010/04/twitter-tools.png 698w" sizes="(max-width: 300px) 100vw, 300px" />
  </p>
  
  <p>
    That&#8217;s it really. I also adapted an <a href="http://www.freshpressthemes.com/twitter-wordpress-theme/">existing Twitter inspired template</a> for WordPress to be even better for tweets (don&#8217;t show title, don&#8217;t show author, permalink post time and so on). And, <a href="http://protocol7.com/tweets">here we go, all my tweets</a>, ready for indexing and saved for posterity. Now all I need to do is to write something useful that is actually worth saving, but that&#8217;s the easy part right :-)
  </p>
</div>