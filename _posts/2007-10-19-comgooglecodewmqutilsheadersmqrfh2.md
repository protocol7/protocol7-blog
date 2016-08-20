---
id: 1531
title: com.googlecode.wmqutils.headers.MQRFH2
date: 2007-10-19T11:52:27+00:00
author: Niklas
layout: post
guid: http://protocol7.com/archives/2007/10/19/comgooglecodewmqutilsheadersmqrfh2/
permalink: /archives/2007/10/19/comgooglecodewmqutilsheadersmqrfh2/
tags:
  - Messaging/JMS
  - MQ
  - Open source
openid_comments:
  - 'a:1:{i:0;s:5:"99429";}'
---
<div class='microid-224f5e96dcc80af5502c90de1539c478018ed304'>
  <p>
    Sometimes, when you&#8217;re out of luck, you need to use the <a href="http://publib.boulder.ibm.com/infocenter/wmqv6/v6r0/index.jsp?topic=/com.ibm.mq.csqzak.doc/csqzak10172.htm">old Base Java API for WebSphere MQ</a>. That is, not JMS. And you might need to create, or even worse, read a RFH2 header. If this is you, you probably loath the mess that is the RFH2 header structure. It&#8217;s a mix of a leading binary structure, followed by zero or more almost-XML structures. I have yet to see a <a href="http://publib.boulder.ibm.com/infocenter/wmqv6/v6r0/topic/com.ibm.mq.csqzak.doc/csqzak10172.htm">complete specification</a>.
  </p>
  
  <p>
    So, what&#8217;s a poor hacker to do. I&#8217;ve written up a utility class for <a href="http://code.google.com/p/wmq-util/wiki/CreatingRfh2Header">creating</a> and <a href="http://code.google.com/p/wmq-util/wiki/ReadingRfh2Header">parsing</a> RFH2 headers as part of the <a href="http://code.google.com/p/wmq-util/">wmq-util library</a> that I&#8217;m doing at work. The aim is simple: make it easy to use RFH2 headers without any risk of screwing up. Enjoy and report back bugs and suggestions.
  </p>
  
  <p>
    Technorati Tags: <a class="performancingtags" href="http://technorati.com/tag/wmq" rel="tag">wmq</a>, <a class="performancingtags" href="http://technorati.com/tag/ibm" rel="tag">ibm</a>, <a class="performancingtags" href="http://technorati.com/tag/java" rel="tag">java</a>, <a class="performancingtags" href="http://technorati.com/tag/wmq-util" rel="tag">wmq-util</a>
  </p>
</div>