---
id: 1521
title: WebSphere MQ message spoofing using confirm-on-arrival reports
date: 2007-08-31T12:17:37+00:00
author: Niklas
layout: post
guid: http://protocol7.com/archives/2007/08/31/websphere-mq-message-spoofing-using-confirm-on-arrival-reports/
permalink: /archives/2007/08/31/websphere-mq-message-spoofing-using-confirm-on-arrival-reports/
tags:
  - MQ
  - Security
---
<div class='microid-5442c09a10807c3c62d98f479b96bff3a8923f0a'>
  <p class="note">
    This post is part of a series I&#8217;m doing on <a href="http://protocol7.com/archives/2007/08/31/websphere-mq-security/">WebSphere MQ security</a>.
  </p>
  
  <p>
    As described in my previous post of in this series, this method of spoofing messages in WebSphere MQ should be fully attributed to T-Rob, famous from the <a href="http://listserv.meduniwien.ac.at/archives/mqser-l.html">WMQ mailing list</a> for his deep knowledge of most odd corners in the WMQ world.
  </p>
  
  <p>
    The exploit described below does not use any bug in WMQ. WMQ in this case works as documented, this is exploit relies on weakly secured WMQ environments.
  </p>
  
  <p>
    As before, I&#8217;ll update this post as I learn new details around this attack or ways of protecting against it.
  </p>
  
  <h3>
    Description
  </h3>
  
  <p>
    WMQ has a feature called <a href="http://publib.boulder.ibm.com/infocenter/wmqv6/v6r0/index.jsp?topic=/com.ibm.mq.csqzal.doc/fg10620_.htm">report messages</a>. These are usually used by a sending application to get a receipt on whether the sent message has arrived, ended up a exception queue or was expirered. To use it is quite simple. The MQMD header (available in all WMQ messages) contain a Report attribute. Set this to the appropriate value and provide a reply queue and you will get receipts for your sent messages. You can also decide on what you want the report message to contain, either just an empty message, the first 100 bytes or the full data of the original message. In all of these, the report message will have a MsgType (in the MQMD) attribute set to the value Report (4) and a non-zero Feedback attribute (also in the MQMD).
  </p>
  
  <p>
    One type of report message is the &#8220;confirm on arrival&#8221; (COA). This report message is sent by WMQ itself when a message successfully arrives on its target queue. As WMQ sends it, it is put using administrative authority.
  </p>
  
  <p>
    This attack could also be done using other report types, like expiration, but COA is the attack the requires the least effort.
  </p>
  
  <p>
    Now, if we get access to putting messages on any queue, for example using a hacked application or a badly secured queue manager, we can easily put a spoofed message with a Report attribute requesting a COA with the full message data. We can provide a reply-to queue and reply-to queue manager for any queue in the entire connected WMQ network. Now imagine that this message contains a spoofed message for some application on the WMQ network. An easy and effective attack unless the receiving application knows to defend itself.
  </p>
  
  <p>
    <img src="http://protocol7.com/wp-content/uploads/2007/08/wmq-spoofed-coa.png" />
  </p>
  
  <h3>
    Protect yourself
  </h3>
  
  <p>
    There is, as far as I know, no way of shutting of report messages in WMQ. It would be a good addition to WMQ security if we would be able to shut of reports on a queue manager and queue basis.
  </p>
  
  <p>
    Sign your messages. Let the sending application digitally sign all messages it send and let the receiving application verify these signatures against known senders. Message with unknown or invalid signatures must be ignored, put on an exception queue and an alert raised.
  </p>
  
  <p>
    Receiving applications should verify that they receive an expected message type. Normally, this would be a Datagram or a Request. All other types, and specifically Reports must be ignored, put on an exception queue and an alert raised. In fact, the built-in WMQ command server does this check and will ignore any messages which is not of the Request type. This shows that IBM is well aware of this exploit and are doing these checks themselves. Without this check in the command server, this exploit would have allowed administering WMQ.
  </p>
  
  <p>
    If using JMS, here is some example code for how to check the message type:
  </p>
  
  <pre>
if(!msg.propertyExists("JMS_IBM_MsgType") || 
    msg.getIntProperty("JMS_IBM_MsgType") == 1 || 
    msg.getIntProperty("JMS_IBM_MsgType") == 8) { 
    // do your stuff 
} else { 
    // run screaming away from this message 
} 
</pre>
  
  <p>
    Note that if you switch to another JMS provider, this code will still work as it first check for the existence of the specific IBM property.
  </p>
  
  <p>
    If your using the Java Base API, this is what you could do:
  </p>
  
  <pre>
if (message.messageType == MQC.MQMT_REQUEST 
        || message.messageType == MQC.MQMT_DATAGRAM) { 
    // do your stuff 
} else { 
    // run screaming away from this message 
} 
</pre>
  
  <p>
    Code for most other WMQ API will work similarly to the Java Base example. If you got example code for any of the other APIs, feel free to send it to me and I&#8217;ll add it to this post.
  </p>
</div>