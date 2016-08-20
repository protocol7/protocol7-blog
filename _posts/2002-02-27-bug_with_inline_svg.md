---
id: 222
title: Bug with inline SVG
date: 2002-02-27T15:11:32+00:00
author: Niklas
layout: post
guid: http://www.protocol7.com/archives/2002/02/27/bug-with-inline-svg/
permalink: /archives/2002/02/27/bug_with_inline_svg/
categories:
  - Uncategorized
tags:
  - Uncategorized
---
<div class='microid-cc597091cc98f8ba6c8b6330aacadb7f77e42bef'>
  <p>
    Laurence Pit (the creator of <a href="http://www.openwiki.com">openwiki</a>) discovered a strange bug concerning inline SVG and Adobe SVG Viewer. I&#8217;ve been looking into it a little bit more, this is basically how it works:<br /> with ASV 3.0 you can inline SVG in XHTML. But, in IE6, if the XHTML <a href="svg/doctypeBug/with.html">has a DOCTYPE</a> (and it must have to be XHTML) the SVG will not work at all. If you simply <a href="svg/doctypeBug/without.html">remove the DOCTYPE</a> it works again. Strange and annoying bug.
  </p>
</div>