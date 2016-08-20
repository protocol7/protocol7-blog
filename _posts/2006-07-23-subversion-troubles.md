---
id: 1259
title: Subversion troubles
date: 2006-07-23T21:31:54+00:00
author: Niklas
layout: post
guid: http://www.protocol7.com/archives/2006/07/23/subversion-troubles/
permalink: /archives/2006/07/23/subversion-troubles/
tags:
  - Subversion
  - Zystems
---
<div class='microid-56741fa49d0efeecbb54b0b141d3929b68089b24'>
  <p>
    Lately, we&#8217;ve been having some issues with Subversion at work. We use SVN for all things that need versioning, mostly code but also documentation and deployed artefacts. Since we&#8217;re a fairly small company its not a huge repository (some 45000 total commits, approximatly 150 commits per day). Now, since begining of June some revisions has gone bad resulting in the following error on checkout or update:
  </p>
  
  <blockquote>
    <p>
      Error REPORT request failed on &#8216;/repos/main/!svn/vcc/default&#8217;<br /> Error REPORT of &#8216;/repos/main/!svn/vcc/default&#8217;: Could not read chunk delimeter:<br /> Error Secure connection truncated
    </p>
  </blockquote>
  
  <p>
    &#8220;svnadmin verify&#8221; outputted the following on examining the affected revision:
  </p>
  
  <blockquote>
    <p>
      &#8220;insn 0 starts beyond the target view position&#8221;
    </p>
  </blockquote>
  
  <p>
    After some Googling I found <a href="http://ian.blenke.com/subversion/fsfs/corruption/repair/fsfsrepair.html">this write-up</a> by Ian C. Blenke, describing the same problem as we see. After some discussion on svn-users and the excellent help by John Szakmeister, his <a href="http://www.szakmeister.net/blog/?page_id=16">fsfsverify</a> tool now catches and fixes our first broken revision. <strike>He is still examining a second broken revision that currently breaks fsfsverify. But, since so far there hasn&#8217;t been any data corruption seen due to this bug I have high hopes for John being able to create a fix.</strike>
  </p>
  
  <p>
    Update: John has now updated fsfsverify to also catch and fix our second broken revision.<br /> So, if you&#8217;re seeing this problem, report it on svn-users, take a backup of your repository and try out John&#8217;s tool.
  </p>
</div>