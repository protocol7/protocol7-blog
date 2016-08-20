---
id: 1517
title: A first look at MA0Y, the HTTP interface for WebSphere MQ
date: 2007-07-12T21:45:36+00:00
author: Niklas
layout: post
guid: http://protocol7.com/archives/2007/07/12/a-first-look-at-ma0y-the-http-interface-for-websphere-mq/
permalink: /archives/2007/07/12/a-first-look-at-ma0y-the-http-interface-for-websphere-mq/
tags:
  - MQ
categories:
  - REST
---
<div class='microid-74e162b66d81748ae2c3332edb19e7ebd2cf5996'>
  <p>
    As has already been <a href="http://hursleyonwmq.wordpress.com/2007/07/05/new-websphere-mq-http-support/">reported</a> in <a href="http://de9644.wordpress.com/2007/07/12/ibm-websphere-mq-bridge-for-http-ma0y-tested/">several</a> <a href="http://marten.gustafson.pp.se/blog/2007/07/03/wmq-http-bridge/">blogs</a>, IBM has released a <a href="http://www-1.ibm.com/support/docview.wss?uid=swg24016142">new supportpac</a> for exposing <a href="http://www.ibm.com/software/integration/wmq/">WebSphere MQ</a> queues and topics as HTTP resources. The supportpac aims at being RESTful, at least that&#8217;s what you are lead to believe from the banner on the main WMQ site.<br /> <img src="http://www-306.ibm.com/software/integration/wmq/images/http_bridge_logo.jpg" />
  </p>
  
  <p>
    However, much like the <a href="http://activemq.apache.org/rest.html">ActiveMQ REST support</a>, the RESTfulness, or even basic HTTP compliance does have it&#8217;s rough edges.
  </p>
  
  <p>
    The supportpac exposes a queue on a URL looking like http://example.com/wmq/msg/queue/FOO. On this resource, three basic operations is allowed:
  </p>
  
  <ul>
    <li>
      POST: will push a new message to the queue
    </li>
    <li>
      GET: will peek at the first message from the queue
    </li>
    <li>
      DELETE: will pop the first message from the queue
    </li>
  </ul>
  
  <p>
    Now, there are several problems here. For example, the GET and DELETE is done at the queue URL, but actually works on a different resource, the message. The way the DELETE is done, the expectation would be to remove the queue itself. And the GET should return some representation of the queue, such as a listing of the available messages. On top of this, <a href="http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html#sec9.1.2">DELETE must be idempotent</a>, however in this case, doing multiple DELETEs will result in very different results (different messages being read). In addition, re-doing a failed DELETE (for example due to being in-doubt because of a network failure) could lead to multiple messages being lost (note that IBM makes it clear that this is the case).
  </p>
  
  <p>
    All that being said, as been shown on <a href="http://permalink.gmane.org/gmane.comp.web.services.rest/6149">rest-discuss lately</a>, designing a queue with the standard HTTP methods is not entirely straight-forward and might lead to a both complex and odd (from a queuing perspective) API. Adding simplicity in the mix, and not supporting assured delivery, the design chosen in the WMQ supportpac might be understandable.
  </p>
  
  <p>
    Besides the issues above, I think a big improvement to the API would be if it supported resource discovery. The examples below describe this, in addition to suggesting a better design for pushing, peeking and popping messages:
  </p>
  
  <ul>
    <li>
      http://example.com/wmq returning a list of the available queue managers
    </li>
    <li>
      http://example.com/wmq/myqm returning a list of the available destinations on that specific queue manager.
    </li>
    <li>
      As discussed above, the http://example.com/wmq/myqm/queue/FOO resource should return a list of available messages on that specific destination. This resource also supports the POST as described above.
    </li>
    <li>
      http://example.com/wmq/myqm/queue/FOO/nextmsg redirecting to the first message of the queue
    </li>
    <li>
      http://example.com/wmq/myqm/queue/FOO/123456789 identifying a specific message and supports the GET and DELETE requests as described above.
    </li>
  </ul>
  
  <p>
    In <a href="http://protocol7.com/archives/2007/06/13/a-restful-queue/#comment-43423">a comment</a> on an <a href="http://protocol7.com/archives/2007/06/13/a-restful-queue/">earlier post here</a>, James Strachan of ActiveMQ notes that he would like to design a fully RESTful API for ActiveMQ. Maybe that could be a chance to dive deeper into this interesting area.
  </p>
  
  <p>
    As noted on the <a href="http://hursleyonwmq.wordpress.com/2007/07/05/new-websphere-mq-http-support/">Hursley WMQ blog</a>, IBM is looking for feedback on the code, so hopefully some of these issues could be taken care of.
  </p>
</div>