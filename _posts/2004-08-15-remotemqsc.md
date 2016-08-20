---
id: 1051
title: RemoteMQSC
date: 2004-08-15T23:45:31+00:00
author: Niklas
layout: post
guid: http://www.protocol7.com/archives/2005/02/23/remotemqsc/
permalink: /archives/2004/08/15/remotemqsc/
tags:
  - Java
  - MQ
---
<div class='microid-504d95c63083c5bbf105ef1faecb9eb333c0edeb'>
  <p>
    I’ve uploaded the first release of a small project of mine, RemoteMQSC. If you have ever used WebSphere MQ you’ve probably used MQ script and the runmqsc (strmqmmqsc on AS400) command. RemoteMQSC does exactly the same thing but for remote MQ servers. RemoteMQSC runs as a MQ client and sends the script commands as escaped PCF messages.
  </p>
  
  <p>
    To run the program, the simplest command is:
  </p>
  
  <p>
    java -jar remotemqsc.jar -hostname yourhost
  </p>
  
  <p>
    The command requires a host name but can also include the following parameters:
  </p>
  
  <p>
    * -channel SOME.CHANNEL<br /> * -port 1881<br /> * -sslciphersuite SSL_RSA_WITH_NULL_MD5<br /> * -userID someuser<br /> * -password secret<br /> * -CCSID 850
  </p>
  
  <p>
    Note that since I’m not allowed to distribute the IBM JAR files you will have to copy them into the RemoteMQSC directory on your own. The required JARs are:
  </p>
  
  <p>
    * com.ibm.mq.pcf.jar<br /> * com.ibm.mq.jar<br /> * connector.jar
  </p>
  
  <p>
    Right now the source code is hosted on my private CVS server so if you want the source code, please send me an email and I’ll send it to you.
  </p>
</div>