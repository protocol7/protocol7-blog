---
id: 1519
title: WebSphere MQ message spoofing using the dead letter queue
date: 2007-08-17T09:52:36+00:00
author: Niklas
layout: post
guid: http://protocol7.com/archives/2007/08/17/websphere-mq-message-spoofing-using-the-dead-letter-queue/
permalink: /archives/2007/08/17/websphere-mq-message-spoofing-using-the-dead-letter-queue/
tags:
  - Messaging/JMS
  - MQ
  - Security
---
<div class='microid-1551e08d70cdf4c9845df3b9b3104f157f47933a'>
  <p class="note">
    This post is part of a series I&#8217;m doing on <a href="http://protocol7.com/archives/2007/08/31/websphere-mq-security/">WebSphere MQ security</a>.
  </p>
  
  <p>
    Security in WebSphere MQ is heavily reliant on applications only being able to put messages where we want them to. Otherwise, an hacked application can be used to send messages where it is not supposed to, for example inserting spoofed messages destined for some other application. As messages commonly contain very important business data and have a high-priviliaged route into applications, spoofing messages can be a very efficient way of hacking.
  </p>
  
  <p>
    Over at the WebSphere MQ mailing list, I <a href="http://permalink.gmane.org/gmane.network.mq.devel/5700">described</a> a simple but somewhat inefficient way of spoofing messages using the dead letter queue. <a href="http://permalink.gmane.org/gmane.network.mq.devel/5701">T-Rob followed</a> that by outlining an even simpler attack using confirm on arrival reports. In this first post, I&#8217;ll try to describe the first exploit and will then follow up with a post describing the exploit described by T-Rob. Please note that none of these two methods rely on any bug in WMQ, the product is working as designed.
  </p>
  
  <p>
    This post is in the interest of <a href="http://www.schneier.com/blog/archives/2007/01/debating_full_d.html">full</a> <a href="http://en.wikipedia.org/wiki/Full_disclosure">disclosure</a>, what you don&#8217;t know is hard to protect yourself against.
  </p>
  
  <h3>
    Spoofing messages using the dead letter queue
  </h3>
  
  <h4>
    Description
  </h4>
  
  <p>
    WMQ uses a shared queue called the dead letter queue as the ultimate destination for messages that can not be delivered. This might be due to many reasons, but the case of interest here is for applications that can not handle a message (due to for example resource problems or data corruption). In many cases, such an application will choose to store away this message on the dead letter queue to be able to continue processing further incoming messages.
  </p>
  
  <p>
    A message stored on the dead letter queue will usually contain a header containing the orginal target queue and queue manager. The purpose of this is to automatically be able to retry the message when whatever the original problem was. The target queue can include the administration queues, or a queue on any other reachable queue manager.
  </p>
  
  <p>
    On a typical system, this queue will be named SYSTEM.DEAD.LETTER.QUEUE. On a queue manager that is shared by multiple applications, a very common practice, this means that this queue might be used by several different applications.
  </p>
  
  <p>
    WMQ also has what is called <a href="http://publib.boulder.ibm.com/infocenter/wmqv6/v6r0/index.jsp?topic=/com.ibm.mq.amqzag.doc/fa15920_.htm">dead letter queue handlers</a>, a process running that monitors the dead letter queue for messages and then, using a <a href="http://publib.boulder.ibm.com/infocenter/wmqv6/v6r0/index.jsp?topic=/com.ibm.mq.amqzag.doc/fa14020_.htm">rules table</a>, decide on what to do with the message. The options includes to retry for a number of times, store it somewhere else, delete it, leave it on the dead letter queue, and so on. A message that can not be successfully retried or deleted will finally be handled by an administrator, for example by fixing the troubling application and the retrying the message.
  </p>
  
  <p>
    Now, if applications has put authority on the dead letter queue, it can simply fake the header containing the original target queue. The dead letter queue handler or a unobservant administrator might then try to retry the message by putting it on the faked target queue.
  </p>
  
  <h4>
    Protect yourself
  </h4>
  
  <p>
    There are a few, more or less, efficient ways of protecting against this exploit. The methods described below are not mutually exclusive, investigate what the most reasonable solution is in your case.
  </p>
  
  <p>
    Don&#8217;t give applications put authority on the dead letter queue. For applications that support it, instead create a specific exception queue for only that specific application. For applications that still requires using the dead letter queue, investigate their behavior if they get an security exception when accessing it. If their failure behavior (probably rolling back the message to the original queue) is acceptable, go with that.
  </p>
  
  <p>
    Let the source application digitally sign its messages and let the target application confirm the signature. This is a efficient method, albeit sometimes hard to implement due to, for example, the use off-the-shelf applications without such support.
  </p>
  
  <p>
    If using a dead letter queue handler, make sure the rules table confirm that the message contain the expected USERID. It should contain the user with which the real source application accesses WMQ. It must not contain the value of any other, possibly hacked application.
  </p>
  
  <p>
    Don&#8217;t retry messages targeted for the command server or any other administrative funtion.
  </p>
  
  <p>
    Let the target application confirm the USERID, in the same fashion as the dead letter queue handler.
  </p>
</div>