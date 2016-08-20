---
id: 1039
title: Subversion
date: 2005-01-23T01:23:06+00:00
author: Niklas
layout: post
guid: http://www.protocol7.com/archives/2005/01/23/subversion/
permalink: /archives/2005/01/23/subversion/
tags:
  - Applications
---
<div class='microid-a797f16d2ff10b0e6691345d8123375b91b7f21c'>
  <p>
    Today I migrated my personal repository (mostly some documents and a few software projects) from CVS to Subversion 1.0. Installation was very smooth:
  </p>
  
  <ol>
    <li>
      apt-get install subversion
    </li>
    <li>
      apt-get install libapache2-svn
    </li>
    <li>
      svnadmin create /data/svnroot
    </li>
    <li>
      chown www-data.www-data /data/svnroot
    </li>
    <li>
      htpasswd2 niklas
    </li>
    <li>
      Configure Apache2 to locate the svnroot
    </li>
    <li>
      Done
    </li>
  </ol>
  
  <p>
    After that I simply imported a snapshot of the files, I didn&#8217;t care all that much about the history of the files, but if I did I&#8217;m sure that the <a href="http://cvs2svn.tigris.org/">migration scripts</a> would work just fine.
  </p>
  
  <p>
    For lots of more information on making this transfer, see <a href="http://www.chiark.greenend.org.uk/~sgtatham/svn.html">this writeup</a> by Simon Tatham, the maintainer of Putty.
  </p>
  
  <p>
    I&#8217;ll post some more later after I&#8217;ve been using svn for some time but so far its looking promising.
  </p>
</div>