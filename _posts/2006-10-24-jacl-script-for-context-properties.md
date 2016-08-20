---
id: 1333
title: JACL script for context properties
date: 2006-10-24T21:32:20+00:00
author: Niklas
layout: post
guid: http://protocol7.com/archives/2006/10/24/jacl-script-for-context-properties/
permalink: /archives/2006/10/24/jacl-script-for-context-properties/
tags:
  - Messaging/JMS
---
<div class='microid-bb7251d36e77271cbdf23acb76101b931fea61c6'>
  <p>
    Couldn&#8217;t find this on Google, so I thought I should post it here. It&#8217;s a JACL script for creating a <a href="http://publib.boulder.ibm.com/infocenter/wasinfo/v6r0/index.jsp?topic=/com.ibm.websphere.pmc.express.doc/concepts/cjj0000_.html">WPM/SIB/JetStream</a> JMS alias destination with <a href="http://publib.boulder.ibm.com/infocenter/wasinfo/v6r0/index.jsp?topic=/com.ibm.websphere.pmc.express.doc/tasks/tjo0050_.html">the magic context property needed to generate a MQRFH2 header</a> when sending messages to MQ.
  </p>
  
  <p>
    <code>
&lt;p>set dest [ $AdminTask createSIBDestination "-bus MyBus -type Alias -name MyQueue -node $nodeName -server $serverName -targetBus MyMQBus -targetName MyMQQueue" ] &lt;/p>
&lt;p>$AdminConfig create SIBContextInfo $dest {{name _MQRFH2Allowed} {type BOOLEAN} {value true}}&lt;/p>
&lt;p></code>
  </p>
</div>