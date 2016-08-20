---
id: 882
title: Adobe SVG Viewer 4
date: 2003-01-25T17:00:51+00:00
author: Niklas
layout: post
guid: http://www.protocol7.com/archives/2003/01/25/adobe-svg-viewer-4/
permalink: /archives/2003/01/25/adobe_svg_viewer_4/
tags:
  - SVG
---
<div class='microid-eefdfa9f38c045bc6c8434c76613da456c49d8cb'>
  <p>
    Some day ago, Ian Tindale, <a href="http://groups.yahoo.com/group/svg-developers/message/25766">posted a message about Adobe Imageviewer</a> which actually turned out to be based on a new version of Adobe SVG Viewer. The viewer is bundled with Acrobat Reader and not directly usable as a browser plugin. <a href="http://groups.yahoo.com/group/svg-developers/message/25781">Adobe&#8217;s Jon Ferraiolo confirmed this the same day</a>
  </p>
  
  <p>
    Of course, some people started playing with it. From a <a href="http://groups.yahoo.com/group/svg-developers/message/25792">PDF posted by Dean Jackson</a> we were able to extract an embedded SVG file that gave some clues.
  </p>
  
  <p>
    <a href="http://www.kevlindev.com">Kevin Lindsey</a> created a minimal PDF that could contain a SVG file and <a href="http://www.kevlindev.com/utilities/index.htm">a script for creating it</a>. He also showed that the new ASV now <a href="http://www.protocol7.com/lab/asv4/cursor.pdf">supports cursors</a> (note: the linked PDF files all require <a href="http://www.adobe.com/products/acrobat/readstep2.html">Acrobat Reader 5.1 including the ImageViewer</a> to work.
  </p>
  
  <p>
    I&#8217;ve done some additional experiments:<br /> Cursors can also be animated (note that if you&#8217;r on a Mac, this will likely crash your browser): <a href="http://www.protocol7.com/lab/asv4/anim_cursor.pdf">example</a>
  </p>
  
  <p>
    And the most exciting news, it supports flowing text: (<a href="http://www.protocol7.com/lab/asv4/flow.pdf">example</a>). The syntax is not exactly that of the lastest SVG 1.2 draft (<code>region</code> instead of <code>flowRegion</code>), but that&#8217;s most likely just a timing issue.
  </p>
  
  <p>
    According to Jon it also supports embedded video. In the PDF the Dean posted you can find traces of a <code>video</code> element in Adobe&#8217;s extension namespace. I have however failed to get it to work. Any clues would be welcome :-)
  </p>
  
  <p>
    If you find out any other differences compared to ASV3, please <a href="mailto:niklas@protocol7.com">email me</a>.
  </p>
</div>