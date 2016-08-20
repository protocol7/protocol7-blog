---
id: 1512
title: Surprised by reality
date: 2007-06-12T22:12:37+00:00
author: Niklas
layout: post
guid: http://protocol7.com/archives/2007/06/12/surprised-by-reality/
permalink: /archives/2007/06/12/surprised-by-reality/
tags:
  - Applications
---
<div class='microid-76e51b0b2f098413dab28b57c139d7ef53128eb8'>
  <p>
    I&#8217;m a big fan of <a href="http://www.jhorman.org/wikidPad/">Wikidpad</a> and use it for most (if not all) of my digital notes (a trusty <a href="http://www.moleskine.com/eng/default.htm">Moleskin</a> does the trick for those analog ones). Today I was in a meeting discussing a set of integrations between a few applications. Pictures was drawn on the whiteboard and I was somewhat desperately trying to convey these into wiki text. The results wasn&#8217;t all that good. This scenario has been played over and over again and I have tried a large number of different replacements for Wikidpad that would be somewhat more &#8220;rich&#8221; in their content, for example <a href="http://office.microsoft.com/en-us/onenote/default.aspx">OneNote</a>. Still, every time I have returned to old, trusted Wikidpad. <br />Now, while in the meeting today I thought that the pictures drawn would be perfect to draw using <a href="http://www.graphviz.org/Gallery/directed/world.html">dot</a> from <a href="http://www.graphviz.org">GraphViz</a>, another favorite of mine. I went into my text editor and hacked up a simple dot file that described that integration scenarios being discussed. When I was about to save the file, it struck me that since it just text it would be better suited to store it right there in the wiki. I thought that some Python (that&#8217;s what Wikidpad is written in) hacker should fairly easily write up some code to render it for me. When I was about to start writing an email begging at people over at the dev list, it actually struck me to look at the extensions already shipped with Wikidpad. Lo and behold, right there is was, <a href="http://wikidpad.python-hosting.com/file/branches/mbutscher/work/extensions/GraphvizClBridge.py">GraphvizClBridge.py</a>. And nicely documented as well. So now I got perfectly beautiful dot images just where I want them. Couldn&#8217;t be happier.
  </p>
</div>