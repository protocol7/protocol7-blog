---
id: 1596
title: RPC getting hot again?
date: 2008-07-31T19:55:50+00:00
author: Niklas
layout: post
guid: http://protocol7.com/?p=1596
permalink: /archives/2008/07/31/rpc-getting-hot-again/
categories:
  - Uncategorized
tags:
  - etch
  - protocol buffers
  - rpc
  - thrift
---
<div class='microid-d708a0bfe2b7ddb74f803d85bf83aa092b20ed7e'>
  <p>
    Not only did <a href="http://www.cio.com/article/print/365513">Cisco</a> see the need <a href="http://steve.vinoski.net/blog/2008/05/22/just-what-we-need-another-rpc-package/">in inventing their own RPC protocol</a>, now they become the third major player in a short time to open source it, or <a href="http://incubator.markmail.org/search/?q=#query:list%3Aorg.apache.incubator.general+page:1+mid:xwy6azpdwqp2xa25+state:results">at least that&#8217;s the aim</a>. The opening of <a href="http://incubator.apache.org/thrift/">Facebook&#8217;s Thrift</a> was pretty much quite. But, as with anything touched by todays Midas, Google&#8217;s <a href="http://code.google.com/p/protobuf/">Protocol buffers</a> stirred <a href="http://steve.vinoski.net/blog/2008/07/11/protocol-buffers-no-big-deal/">a</a> <a href="http://www.innoq.com/blog/st/2008/07/google_can_have_stupid_ideas_t.html">bigger</a> <a href="http://steve.vinoski.net/blog/2008/07/13/protocol-buffers-leaky-rpc/">debate</a> <a href="http://blogs.tedneward.com/2008/07/11/So+You+Say+You+Want+To+Kill+XML.aspx">on</a> the merits of RPC.
  </p>
  
  <p>
    I think this is an area that merits some further discussion. By now, we&#8217;ve figured out that RPC is a bad fit in heterogeneous, cross-domain integrations. But, in the case you own both ends of the wire and you need some serious throughput and low latency communication, these types of protocols is likely a better fit. At least in the mega environments some of the web companies run these days. It&#8217;s interesting to follow along with the rapid development of such infrastructure, even though they are out of the hands of most of us. At least for now.
  </p>
  
  <p>
    So, with all three combatants now in the open. Let the fight begin.
  </p>
</div>