---
id: 1540
title: You learn something new every day
date: 2007-11-27T17:47:48+00:00
author: Niklas
layout: post
guid: http://protocol7.com/archives/2007/11/27/you-learn-something-new-every-day/
permalink: /archives/2007/11/27/you-learn-something-new-every-day/
tags:
  - MQ
---
<div class='microid-ee876bfafaf5aa7016984d2bbf517044a49a9503'>
  <p>
    Looks like <a href="http://www-1.ibm.com/support/docview.wss?uid=swg21288579">IBM added automatic purging of expired messages on distributed platforms in WebSphere MQ 6.0</a>. The <a href="http://http://publib.boulder.ibm.com/infocenter/wmqv6/v6r0/index.jsp?topic=/com.ibm.mq.csqzak.doc/js01159.htm">documentation</a> seems to fail mentioning this change so I had no clue. This is a great addition as for queues with frequent PUTs and rare GETs (e.g. with a slow or downed receiver), expired messages might build up fast.
  </p>
  
  <p>
    The details of how and when the queue manager does the purging is not mentioned, only that you&#8217;re not guaranteed that it it will purge as fast as you want (which makes sense). Also ,the REFRESH QMGR TYPE(EXPIRY) command available on z/OS is not supported. It would explicitly purge messages on the named (including wild cards) queues. I hope they will get around to doing that as it will be a lot easier then doing GETs on all queues with possible expired messages when you really need to know that messages are purged..
  </p>
  
  <p>
  </p>
</div>