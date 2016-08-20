---
id: 835
title: SharpVectorGraphics 0.2.4
date: 2002-12-10T11:26:23+00:00
author: Niklas
layout: post
guid: http://www.protocol7.com/archives/2002/12/10/sharpvectorgraphics-024/
permalink: /archives/2002/12/10/sharpvectorgraphics_024/
tags:
  - SVG
---
<div class='microid-c1e6b1235cb66518fb2a0896e9674e86f3b2ac50'>
  <p>
    Last night I uploaded and released <a href="http://sourceforge.net/project/showfiles.php?group_id=46621&release_id=127118">version 0.2.4 of SharpVectorGraphics (SVG#)</a>, an implementation of SVG 1.0/1.1 in .NET. The packages includes support for the SVG DOM, a renderer, SVG picture component for WinForms and a minimal browser. The change log looks like this:
  </p>
  
  <ul>
    <li>
      gzip support (using NZipLib)
    </li>
    <li>
      Re-arranged the path code to make it much simpler to work with
    </li>
    <li>
      Added support for color-interpolation==&#8221;linearRGB&#8221; on linear gradients
    </li>
    <li>
      Added basic marker support. A clipping bug and some rotation calculation fixes left to do.
    </li>
    <li>
      Added support for elements
    </li>
    <li>
      Handling of external resources for elements improved
    </li>
    <li>
      Generalized and handling
    </li>
    <li>
      Added support for inline SVG images (with the element)
    </li>
    <li>
      Added support for angles in SVG
    </li>
    <li>
      Improved and simplified viewPort and viewBox handling
    </li>
    <li>
      Added SvgWindow as the root object (according the the proposal in SVG 1.2)
    </li>
    <li>
      Fixed gradients bug
    </li>
    <li>
      Fixed so that presentation attributes with !important are ignored (testcase styling-pres-01-t.svg)
    </li>
    <li>
      Added support for locally stored DTDs (LocalDtdXmlUrlResolver.cs)
    </li>
    <li>
      Structured lots of code (added documentation and regions)
    </li>
    <li>
      Improved cache handling (but much more to do)
    </li>
    <li>
      Corrected information in the assembly info
    </li>
    <li>
      Tons of minor fixes
    </li>
  </ul>
</div>