---
id: 1545
title: Decent WP setup
date: 2007-12-26T22:28:57+00:00
author: Niklas
layout: post
guid: http://protocol7.com/archives/2007/12/26/decent-wp-setup-2/
permalink: /archives/2007/12/26/decent-wp-setup-2/
tags:
  - protocol7
  - Subversion
  - Weblogging
  - Wordpress
---
<div class='microid-e1f07e6739f2520017ed86f05c92b26d1d06fe73'>
  <p>
    Is this thing on? protocol7 has been broken for a few days due to an upgrade at my hosting and me being lazy over the holidays and not reporting it. Now, the Joyent support has fixed it and we should be back online.
  </p>
  
  <p>
    This event reminded me that I needed to revisit my site configuration. I keep the entire site (except for the stuff that MySQL stores for me) in Subversion. The live site is simply a checked out working copy. Whenever I need to make an update, I do that locally on my laptop and commit the change to SVN. Then run a simple <code>svn up</code> on my server and it&#8217;s all done. This setup gives me a lot of confidence in knowing that all changes are safely stored and I can easily retrieve old working versions to rollback any bad update. In this case, this helped me a lot since one of the problems was a file that was mysteriously missing on the live site. <code>svn up</code> fixed that immediately.
  </p>
  
  <p>
    I&#8217;ve also used the <a href="http://codex.wordpress.org/Installing/Updating_WordPress_with_Subversion">SVN installation method for WordPress</a>. However, my customizations has been troublesome. Since SVN can not handle overlapping working copies, the files below the WP checkout could not be stored in my SVN. This included my themes and plugins, the files that I spend most time on customizing. No good.
  </p>
  
  <p>
    Today I spent some time on fixing this. Please note that I know next to nothing about PHP.
  </p>
  
  <h2>
    WP installation
  </h2>
  
  <p>
    I now include WP automatically in my checkout using the <a href="http://svnbook.red-bean.com/en/1.0/ch07s03.html">svn:externals</a> property. This means, that wherever I check out the site, SVN will pull down the version of WP I currently run.<br /> <code>svn propset svn:externals "wp http://svn.automattic.com/wordpress/tags/2.3.1"</code>
  </p>
  
  <h2>
    Plugins
  </h2>
  
  <p>
    Plugins are normally kept in wp-content/plugins beneath the WP installation. Again, this means I can not store these in my SVN. However, the plugins directory can be customized by setting the PLUGINDIR variable. Create a directory in your site root <code>wp-plugins</code> and put this in your wp-config.php:<br /> <code>define('PLUGINDIR', '../wp-plugins'); // no leading slash, no trailing slash</code>
  </p>
  
  <p>
    Then, put all your plugins in wp-plugins and store them in SVN like normal. I pull down any plugin I can using svn:externals, currently Akismet and the OpenID plugin.
  </p>
  
  <h2>
    Themes
  </h2>
  
  <p>
    Themes are normally stored in wp-content/themes. To customize this path, you need to use a different method from plugins. The idea is to use add_filter to create a filter that changes the path. However, there are currently some issues with this approach (for example image paths in the WP admin GUI not using the filtered paths but instead handcrafting them) so I had to use a workaround. I&#8217;ve created a wp-themes directory in the site root, put my themes in it and stored it in SVN. Then, I create soft links using <code>ln -s</code> to link the themes into wp-content/themes. I&#8217;ll continue investigating this issue with the WP developers to see if a better solution is possible.
  </p>
  
  <h2>
    wp-config.php
  </h2>
  
  <p>
    wp-config.php must be kept under the WP installation directory. Again, I use soft links to keep my original copy in a custom directory and under SVN control. Note that as part of wp-config.php, WP detects its installation directory. When using a soft link, it will find the wrong root directory. Instead, I have changed wp-config.php to set the correct root directory explicitly:<br /> <code>define('ABSPATH', '/absolute/path/to/wp/');</code>
  </p>
  
  <p>
    Again, not exactly what you would like, but does the work.
  </p>
  
  <h2>
    Site installation
  </h2>
  
  <p>
    Installing or restoring the site can now be done using the following commands<br /> <code>svn checkout http://example.com/my/svn/repos .&lt;br />
ln -s wp-themes/mytheme wp/wp-content/themes/mytheme&lt;br />
ln -s wp-custom/wp-config.php wp/wp-config.php</code>
  </p>
  
  <p>
    Upgrading WP is done by changing the svn:externals property and then running <c>svn up</c>. Dead simple.
  </p>
  
  <p>
    Technorati Tags: <a class="performancingtags" href="http://technorati.com/tag/wordpress" rel="tag">wordpress</a>, <a class="performancingtags" href="http://technorati.com/tag/wp" rel="tag">wp</a>, <a class="performancingtags" href="http://technorati.com/tag/svn" rel="tag">svn</a>
  </p>
</div>