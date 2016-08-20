---
id: 1649
title: WAS plugin for Nagios
date: 2009-06-03T22:41:13+00:00
author: Niklas
layout: post
guid: http://protocol7.com/?p=1649
permalink: /archives/2009/06/03/was-plugin-for-nagios/
categories:
  - Uncategorized
tags:
  - jms
  - monitoring
  - nagios
  - pmi
  - was
  - websphere
---
<div class='microid-98bf4e49c919d9c32c42a2a90b4be6debb1dc8da'>
  <p>
    At one on my current <a href="http://callistaenterprise.se/">work</a> assignments, we use Nagios (or more specifically, the <a href="http://www.op5.se/op5/produkter/monitor">OP5 packaged Nagios</a>) for all our infrastructure and application monitoring. We also use a fair amount on WebSphere Application Server instances. Thus, we needed to monitor WAS from Nagios, including some WAS internals like heap size and connection pool sizes. Looking around the Tubes, we failed to find any decent Nagios plugin for WAS, so it turned out I had to write one myself. Since the customer has chosen to open source these types of projects, the code is <a href="http://code.google.com/p/nagios-was/">now available</a> over at Google Code under an ASL 2.0 license.
  </p>
  
  <p>
    The plugin will connect to the WAS JMX interface and uses PMI statistics as the source of data. The API for this is pretty horrible, and based on the lack of discussions around it on the web, I presume not that frequently used. But, at least it provides us with the information we need.
  </p>
  
  <p>
    Currently, the plugin support monitoring <a href="http://code.google.com/p/nagios-was/wiki/MonitorJvmHeapsize">JVM heap size</a>, <a href="http://code.google.com/p/nagios-was/wiki/MonitorThreadPools">thread pools</a>, <a href="http://code.google.com/p/nagios-was/wiki/MonitorJdbcConnectionPools">JDBC connection pools</a> and <a href="http://code.google.com/p/nagios-was/wiki/MonitorLiveSessions">live sessions</a>. Lots of other things could potentially be monitored, but this was what we needed. The plugin also supports <a href="http://nagiosplug.sourceforge.net/developer-guidelines.html#AEN201">Nagios performance data</a>, meaning Nagios will provide pretty graphs for your pleasure. We use this a lot to investigate trends like what happens during traffic peaks, long term application behavior or effects of improvements made in applications.
  </p>
  
  <p>
    Getting started is pretty simple, you currently need to download the source code and use Maven to build it into a JAR. You also need to <a href="http://code.google.com/p/nagios-was/wiki/InitialConfiguration">configure a properties file with information on how to connect to your WAS server</a>. After that, it works like any other Nagios plugin.
  </p>
  
  <p>
    The plugin has been tested on WAS 6.1 running in non-clustered environments.
  </p>
  
  <p>
    If you&#8217;re interested in improving on the plugin, feel free to <a href="mailto:niklas@protocol7.com">get in touch</a> and we&#8217;ll most likely grant you commit rights on the project. There are many areas where the code could be improved as well as extended to support additional stuff to monitor, like JMS connection pools or HTTP response times. Also, support for clustered WAS setups and other WAS versions would be most welcome.
  </p>
</div>