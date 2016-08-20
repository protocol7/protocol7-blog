---
id: 866
title: XHTML as a storage format
date: 2003-01-12T01:52:18+00:00
author: Niklas
layout: post
guid: http://www.protocol7.com/archives/2003/01/12/xhtml-as-a-storage-format/
permalink: /archives/2003/01/12/xhtml_as_a_storage_format/
tags:
  - HTML/XHTML
---
<div class='microid-779c0ef0e9931bd51267e5e52f9f5e44d384e292'>
  <p>
    <a title="Simon Willison: Archive for 6th January 2003" href="http://simon.incutio.com/archive/2003/01/06/xhtmlIsJustFine#pingbacks">Simon Willison argues that XHTML works good as the storage format for your content.</a> This is exactly the type of thoughts I had when I decided to re-build protocol7 some time ago. Before, I had a home-made XML format that I used to store all my content. This was then transformed using XSL-T to the HTML on the site. As time had passed, my XML format had grown to handle all my different needs, but what I was doing all along was to build my own copy of XHTML.
  </p>
  
  <p>
    So, for the current version of protocol7 I keep all content in XHTML directly. When I need to do site-wide changes I have a XSL-T based tool that I run on all files automatically. Works perfect for me and I would recommend anyone to try it for your static content.
  </p>
</div>