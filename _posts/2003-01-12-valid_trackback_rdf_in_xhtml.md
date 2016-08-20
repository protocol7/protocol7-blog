---
id: 867
title: Valid trackback RDF in XHTML
date: 2003-01-12T02:26:24+00:00
author: Niklas
layout: post
guid: http://www.protocol7.com/archives/2003/01/12/valid-trackback-rdf-in-xhtml/
permalink: /archives/2003/01/12/valid_trackback_rdf_in_xhtml/
tags:
  - Weblogging
---
<div class='microid-df5687cb9351bdaa6f27a6c4b0d48478f9fe012c'>
  <p>
    Moveable type can automatically ping other sites that I reference in my posts with their technology called <a href="http://www.moveabletype.org/trackback/">trackback</a>. To do the auto-discovery of the trackback URL <a href="http://www.movabletype.org/docs/mttrackback.html#autodiscovery%20of%20trackback%20ping%20urls">it uses RDF embedded in your HTML.</a> Now, the problem with this is that you can&#8217;t just throw in anything in HTML and expect it to validate since RDF elements are totally unknown in the (X)HTML DTDs. One trick around this is to include the RDF as comments, but I think this suck since it makes the whole idea of having markup pretty useless.
  </p>
  
  <p>
    So, today I set out to write a DTD that can be used to keep my markup valid and still make it possible to include the RDF tags. So far, <a href="http://www.protocol7.com/lab/xhtml_trackback/xhtml_trackback.html">my experiment looks like this. (view source)</a>. This file validates using XML-Spy and I belive it&#8217;s valid XML. However, <a href="http://validator.w3.org/check?uri=http%3A%2F%2Fwww.protocol7.com%2Flab%2Fxhtml_trackback%2Fxhtml_trackback.html">the W3C validator reports it as non-valid but fails to find any errors.</a>
  </p>
  
  <p>
    If you find any errors or improvements please <a href="mailto:niklas@protocol7.com">contact me</a>.
  </p>
  
  <p>
    After doing this I discovered that <a href="http://philringnalda.com/archives/002252.php">Phil Ringnalda has done a similar experiment.</a> He also pointed to <a href="http://infomesh.net/2002/rdfinhtml/#embedNoValidate">this document which calls our methods &#8220;eschew validation&#8221;</a>. When reading this I found that they also proposed <a href="http://infomesh.net/2002/rdfinhtml/#link">a different method</a>, simply using links with a special <code>rel</code> attribute. This is a wonderful way of doing it! Won&#8217;t bloth the (X)HTML and won&#8217;t require any changes to the DTDs. Lets hope that support for it will be included in future Moveable type versions.
  </p>
</div>