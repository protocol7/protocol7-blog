---
id: 1620
title: Filtering WebSphere Message Broker logs on Linux
date: 2009-02-10T22:12:27+00:00
author: Niklas
layout: post
guid: http://protocol7.com/?p=1620
permalink: /archives/2009/02/10/filtering-websphere-message-broker-logs-on-linux/
categories:
  - Uncategorized
tags:
  - syslog
  - syslog-ng
  - websphere
  - websphere message broker
  - wmb
---
<div class='microid-b60bcf5a6b517e8c014c8249c41271f406465926'>
  <p>
    On Linux/Unix, WebSphere Message Broker uses the <a href="http://en.wikipedia.org/wiki/Syslog">syslog daemon</a> for its error logging. While arguable the right thing to do, it&#8217;s a mess having application errors mixed up with kernel messages and what not. However, last week, two guys at work set up a clever solution to this problem, using the powerful <a href="http://en.wikipedia.org/wiki/Syslog-ng">syslog-ng</a>. This is all <a href="http://www.linkedin.com/pub/dir/gustav/sinder">Gustav</a> and <a href="http://www.facebook.com/people/Christian_Otback/737285427">Christians</a> work, I merely publish it for others to be able to re-use.
  </p>
  
  <p>
    In the syslog configuration file /etc/syslog-ng/syslog-ng.conf.in, add a filter that matches messages from WMB:
  </p>
  
  <pre><code>
filter f_wmb        { match('^WebSphere Broker'); };
</code></pre>
  
  <p>
    This will allow for catching all messages from WMB. Now, create a destination where you want your WMB messages to go:
  </p>
  
  <pre><code>
destination wmb { file("/var/log/wmb/messages" group(mqm) perm(0644)); };
</code></pre>
  
  <p>
    In this case, we set the group to be mqm, simply because that&#8217;s the group our developers belong to (yeah, that might be a bad idea, but that&#8217;s the topic of another post).
  </p>
  
  <p>
    Now, connect the destination to the filter:
  </p>
  
  <pre><code>
log { source(src); filter(f_wmb); destination(wmb); };
</code></pre>
  
  <p>
    With this setup, all messages coming from WMB will end up in the file /var/log/wmb/messages. To keep /var/log/messages clean, we might also want to strip out WMB messages:
  </p>
  
  <pre><code>
filter f_messages   { not facility(news, mail) and not filter(f_iptables) and not filter(f_wmb); };
</code></pre>
  
  <p>
    This line might look slightly different on your OS, however, the general idea is to add the negated f_wmb filter.
  </p>
  
  <p>
    Now, restart the syslog-ng daemon and you should see your WMB message starting to gather in your new file:
  </p>
  
  <pre><code>
/etc/init.d/syslog restart
</code></pre>
  
  <p>
    In addition to this, we have also set up an Apache HTTPD server to serve up the WMB log file over HTTP, making access to the log trivial for our developers. All in all, I find this very useful. You might also argue that with this knowledge, using the log4j <a href="http://logging.apache.org/log4j/1.2/apidocs/org/apache/log4j/net/SyslogAppender.html">SyslogAppender</a> might be a better idea that our usual RollingFileAppender.
  </p>
</div>