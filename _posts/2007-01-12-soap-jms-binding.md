---
id: 1414
title: SOAP JMS binding
date: 2007-01-12T23:28:14+00:00
author: Niklas
layout: post
guid: http://protocol7.com/archives/2007/01/12/soap-jms-binding/
permalink: /archives/2007/01/12/soap-jms-binding/
tags:
  - Messaging/JMS
  - Standards
  - WS
---
<div class='microid-5bfea382d4b11ccbb7f4c173dde00e08f9269787'>
  <p>
    Looks like <a href="http://mail-archives.apache.org/mod_mbox/ws-axis-dev/200701.mbox/%3c80A43FC052CE3949A327527DCD5D6B27020FB65C@MAIL01.bedford.progress.com%3e">the big guys finally got their act together</a> and wrote both a specification for <a href="http://mail-archives.apache.org/mod_mbox/ws-axis-dev/200701.mbox/raw/%3C80A43FC052CE3949A327527DCD5D6B27020FB65C@MAIL01.bedford.progress.com%3E/2">JMS IRI format</a> and a <a href="http://mail-archives.apache.org/mod_mbox/ws-axis-dev/200701.mbox/raw/%3C80A43FC052CE3949A327527DCD5D6B27020FB65C@MAIL01.bedford.progress.com%3E/3">SOAP JMS binding</a> (<a href="http://netzooid.com/blog/2007/01/12/jms-soap-binding-and-iri-scheme-released-from-bea-ibm-sonic-and-tibco/">via Dan Diephouse</a>). Now, I&#8217;m certainly not the right person to judge the quality of the SOAP binding, but I do like the fact that there might actually be one soonish.
  </p>
  
  <p>
    On the IRI format, its currently only based on using JNDI for identifying the connection factory and destination. However, with JNDI falling out a fashon the last couple of years and JMS commonly running outside the container, I find this a bit lacking. However, the spec leaves some leeway with the following quote:
  </p>
  
  <blockquote>
    <p>
      JMS relies heavily on JNDI for interoperable functionality (vendor extensions may provide alternate means of acquiring a javax.jms.Destination, but only JNDI is interoperably specified).
    </p>
  </blockquote>
  
  <p>
    That only covers the destination, not the connection factory. I would prefer that the spec more clearly allowed for both JNDI based and a more &#8220;freeform&#8221; syntax that&#8217;s up to providers to define. How about:
  </p>
  
  <blockquote>
    <p>
      jms:jndi://connectionFactoryName/destinationName?params
    </p>
  </blockquote>
  
  <p>
    and (for MQ in this example):
  </p>
  
  <blockquote>
    <p>
      jms:wmq://queueManagerName/queueOrTopicName?params
    </p>
  </blockquote>
  
  <p>
    <a href="http://www.activemq.org/site/tcp-transport-reference.html">ActiveMQ</a> and WebSphere MQ&nbsp;already has defined similar URL formats that could be adapted. JMS is inherently not interoperable between different providers anyway, so having these provider specific URLs wouldn&#8217;t hurt. And it would allow using them without having a JNDI implementation around.
  </p>
</div>