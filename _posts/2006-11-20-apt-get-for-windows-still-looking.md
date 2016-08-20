---
id: 1364
title: 'apt-get for Windows &#8211; still looking'
date: 2006-11-20T00:13:08+00:00
author: Niklas
layout: post
guid: http://protocol7.com/archives/2006/11/20/apt-get-for-windows-still-looking/
permalink: /archives/2006/11/20/apt-get-for-windows-still-looking/
tags:
  - Applications
---
<div class='microid-d1cb733edea901d12b915c2ebdba2f5a792cb18a'>
  </p> 
  
  <p>
    Almost a year ago <a href="http://protocol7.com/archives/2006/01/07/google-pack-apt-get-for-windows/">I wrote a piece on Google Pack</a>, suggesting it would be the apt-get for Windows. Well, turned out that nothing much happened about that. So far all there is in the Pack repository is the stuff that was in there from day one, and now also Skype (however it doesn’t seem to be available in Sweden, funny as it was built by a swedish guy). Not a lot of progress in 11 months. So, I went googling for alternatives. Found two that looks active: <a href="http://windows-get.sourceforge.net/index.php">win-get</a> and <a href="http://installpad.com/">InstallPad</a>. win-get looks most promising as they actually got a <a href="http://windows-get.sourceforge.net/listapps.php">fairly large repository</a>, but the activity there seems low (for example, <a href="http://windows-get.sourceforge.net/viewrequests.php">Firefox 2.0 is still not in the main repos</a>). There are also other issues, most notably lack of automatic upgrades to what you already got installed.
  </p>
  
  <p>
    So what’s holding back open-source developers from creating a strong apt-get alternative for Windows? Like on Linux, it will require strong governance around the packaging. But that’s perfectly doable. Another problem is that Windows applications are not as easy to install silently as their Linux counterparts. All types of funky <acronym>GUI</acronym> installers exists and judging from the win-get repos there are quite a few that lacks a silent install option. Even so, it is possible to create your own installers that fixes this problem. At work, our sister company <a href="http://www.zipper.se/?iLanguageID=2">Zipper</a> does exactly this in there commercial <a href="http://www.zipper.se/concept/">FastTrack</a> and <a href="http://www.zipper.se/appline/index.asp">AppLine</a>&nbsp;products. FastTrack is apt-get for Windows inside your firewall and works quite well.
  </p>
  
  <p>
    And, I really don’t get it why Google released Pack and then just seems to have lost all interest in it. They still have an outstanding possibility of getting open-source applications to the masses, and in a good and controlled fashion. That would certainly be very competitive with Microsoft.
  </p>
  
  <p>
    I would be very interested in hearing about additional solutions in the area as I’m sure there a quite a few around that my Google searches has found.
  </p>
</div>