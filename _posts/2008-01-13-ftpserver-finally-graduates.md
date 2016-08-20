---
id: 1550
title: FtpServer finally graduates
date: 2008-01-13T21:05:58+00:00
author: Niklas
layout: post
guid: http://protocol7.com/archives/2008/01/13/ftpserver-finally-graduates/
permalink: /archives/2008/01/13/ftpserver-finally-graduates/
tags:
  - Apache
  - FtpServer
---
<div class='microid-d2143dece378d9d16cf9666aa38fdc0807044060'>
  <p>
    After way to long time in the <a href="http://incubator.apache.org/">Apache Incubator</a>, one of the open-source projects in which I&#8217;m involved, <a href="http://mina.apache.org/ftpserver.html">FtpServer</a> has finally graduated. Our new home is as a subproject under <a href="http://mina.apache.org/">Apache MINA</a>. MINA, being one of my favorite projects, feels like the perfect home. Ever since I wrote an FtpServer <a href="http://mina.apache.org/ftpserver-listeners.html">Listener</a> implementation based on MINA, I&#8217;ve been amazed by how well design the API is. <br />Since the FtpServer community recently voted to drop our support for Java 1.4, that means we can drop our blocking IO implementation. So, I&#8217;m currently in the progress of rewriting our code to make full use of MINA, rather than treating as yet another IO API. Its been great. I&#8217;ve been able to drop a large set of ill-designed classes which should make our code significantly easier to work with.<br />Being part of MINA also means that we will be more visible to more developers, something that will hopefully help us build a larger community. The future for the project is looking bright.
  </p>
  
  <p>
    Technorati Tags: <a class="performancingtags" href="http://technorati.com/tag/mina" rel="tag">mina</a>, <a class="performancingtags" href="http://technorati.com/tag/ftpserver" rel="tag">ftpserver</a>, <a class="performancingtags" href="http://technorati.com/tag/apache" rel="tag">apache</a>
  </p>
</div>