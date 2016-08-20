---
id: 1064
title: SVG enabled
date: 2005-05-03T23:41:28+00:00
author: Niklas
layout: post
guid: http://www.protocol7.com/archives/2005/05/03/svg-enabled/
permalink: /archives/2005/05/03/svg-enabled/
tags:
  - Standards
  - SVG
---
<div class='microid-3e804dd6214b3d5890072445b8a426545eaa6325'>
  <p>
    <a href="http://weblogs.mozillazine.org/tor/archives/2005/05/20050502_weekly.html">Tor</a> has checked in some of the final missing pieces for fully enabling SVG in Firefox 1.1. First, <a href="http://bonsai.mozilla.org/cvsview2.cgi?diff_mode=context&#038;whitespace_mode=show&#038;subdir=mozilla/toolkit/mozapps/installer&#038;command=DIFF_FRAMESET&#038;file=package-name.mk&#038;rev1=1.3&#038;rev2=1.4&#038;root=/cvsroot">the special build names has been removed</a> (you know, for example with -svg-gdiplus) and <a href="http://bonsai.mozilla.org/cvsview2.cgi?diff_mode=context&#038;whitespace_mode=show&#038;root=/cvsroot&#038;subdir=mozilla/modules/libpref/src/init&#038;command=DIFF_FRAMESET&#038;root=/cvsroot&#038;file=all.js&#038;rev1=3.571&#038;rev2=3.572">SVG has been enabled</a> (you now longer have to change the svg.enabled property to see SVG). This is very cool! We are now close to finally getting good (albeit not yet perfect) SVG support in the <a href="http://www.mozilla.org/firefox">second</a> and <a href="http://www.opera.com">third</a> most prevalent browsers out there (I have no hopes for native support in IE). SVG 1.1 (especially mixed in the same document/DOM as (X)HTML) is a powerful tool in the web developers toolbox and this might actually make quite a difference.
  </p>
  
  <p>
    Now, how long until Google Maps comes in SVG?
  </p>
</div>