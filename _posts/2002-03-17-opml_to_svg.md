---
id: 272
title: OPML to SVG
date: 2002-03-17T02:55:32+00:00
author: Niklas
layout: post
guid: http://www.protocol7.com/archives/2002/03/17/opml-to-svg/
permalink: /archives/2002/03/17/opml_to_svg/
tags:
  - SVG
---
<div class='microid-488f8cd5f331b357788b27e09a86fbcab7b9446b'>
  <p>
    I got this idea from a a Flash site (<em>edit: fazal helped me, it&#8217;s <a href="http://www.relevare.com">http://www.relevare.com</a></em>). They have a really nice navigation that is a very good way of visualizing a tree view in a limited area. So, I thought, this would be a perfect way to take a <a href="http://www.opml.org">OPML</a> file and view it using SVG. So, here it is (this is a small example):<br /> <a href="/experiments/svg/opml_to_svg/p7.xml">OPML file</a><br /> <a href="/experiments/svg/opml_to_svg/opml.xsl">XSLT file</a><br /> <a href="/experiments/svg/opml_to_svg/default.svg">Resulting SVG file</a> (you need the <a href="http://www.adobe.com/svg">Adobe SVG Viewer 3.0</a> to see this, animation does not work in Firefox, please email me if you fix it)
  </p>
  
  <p>
    There are a few limitations when using this: it&#8217;s best to have 4 outline elements as children of the body and max 7 outline elements as children of another outline. And texts can not be to long or they won&#8217;t fit. Otherwise it works pretty good. If you use it, please give me your link :-)
  </p>
</div>