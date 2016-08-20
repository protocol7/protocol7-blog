---
id: 1584
title: Custom SSL factory
date: 2008-05-31T13:01:21+00:00
author: Niklas
layout: post
guid: http://protocol7.com/?p=1584
permalink: /archives/2008/05/31/custom-ssl-factory/
categories:
  - Uncategorized
tags:
  - ibm
  - jms
  - ssl
  - wmq
---
<div class='microid-b3b58ac4a5ab4290a24a7508c27275f395270288'>
  <p>
    I&#8217;ve been having this code around for a long time but never seemed to get the time to publish it. Some time ago one of my colleagues asked for a similar solution which finally got me cleaning up the code and publishing it.
  </p>
  
  <p>
    Lets have a look at the problem at hand. Using SSL sockets with most Java APIs means setting a bunch of system properties, <a href="http://java.sun.com/j2se/1.5.0/docs/guide/security/jsse/JSSERefGuide.html#Customization">javax.net.ssl.keyStore</a> and friends. Here be dragons. Using the system properties are in most cases a horrible idea. First of all, the JRE implementation is completely silent on any issues found when it tries to use these system properties, for example due to the key store file path being incorrect. Instead, the SSL handshake will fail in wondrous ways. This will in no way tell you what the real problem is unless you dive into the SSL trace logs. And that&#8217;s not an exercise I would recommend for anyone that doesn&#8217;t enjoy tedious log files and SSL internals.
  </p>
  
  <p>
    In addition, using system properties means the same keystore and truststore must be used for the entire JVM, at least if your application is multithreaded. Want to use different keys for different connections. No can do.
  </p>
  
  <p>
    However, some cases the API will allow for providing a custom SSL socket factory. WebSphere MQ is an example of such an API. As described in <a href="http://hursleyonwmq.wordpress.com/2007/03/08/custom-sslsocketfactory-with-wmq-base-java/">this post by Peter Broadhurst</a>, you can quite easily provide such a custom socket factory with the benefit of getting much improved exceptions if anything goes wrong.
  </p>
  
  <p>
    So, I took some code I had since before, merged it with Peters code and <a href="http://wmq-util.googlecode.com/svn/wmq-util/trunk/src/main/java/com/googlecode/wmqutils/ssl/PojoSslSocketFactoryFactory.java">got the following</a>. You use it like this.
  </p>
  
  <pre>
<code>
        MQQueueConnectionFactory qcf = new MQQueueConnectionFactory();
        qcf.setQueueManager("MYQM");
        qcf.setHostName("localhost");
        qcf.setChannel("SYSTEM.ADMIN.SVRCONN");
        qcf.setSSLCipherSuite(CipherSuite.NULL_SHA);
        qcf.setTransportType(1);
        
        File ks = new File("mykeystore.jks");
        
        // create our factory
        PojoSslSocketFactoryFactory sf = new PojoSslSocketFactoryFactory();
        // setting only the key store means that 
        // it will also be used as the truststore
        sf.setKeyStore(ks);
        sf.setKeyStorePassword("secret");
        
	  // create the socket factory
        qcf.setSSLSocketFactory(sf.createSocketFactory());
        
        Connection conn = qcf.createConnection();
</code>
</pre>
  
  <p>
    Pretty damn easy. And a huge improvement for those who like getting told what&#8217;s wrong with ones configuration. Using the code above, you can also use different key stores within the same JVM.
  </p>
  
  <p>
    The code is available as part of the <a href="http://wmq-util.googlecode.com">wmq-util project</a>, however it is generic and could be used in most applications using SSL sockets where you would normally used the system properties.
  </p>
  
  <p>
    Now we can only hope that, for example, IBM starts using something similar in the WMQ Explorer and WMB Toolkit to make SSL issues easier to debug.
  </p>
  
  <p>
    If anyone is interested, I also got the code to make it possible to have multiple keys in the same key store and configure the one needed for each connection. I haven&#8217;t yet integrated it with the above code but if there is any interest I&#8217;ll do that as well.
  </p>
</div>