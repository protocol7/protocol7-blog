---
id: 1588
title: Basic Constraints on WebSphere MQ CA certificates
date: 2008-06-29T21:45:39+00:00
author: Niklas
layout: post
guid: http://protocol7.com/?p=1588
permalink: /archives/2008/06/29/basic-constraints-on-websphere-mq-ca-certificate/
categories:
  - Uncategorized
tags:
  - ca
  - certificate
  - websphere
  - wmq
---
<div class='microid-7bbb260fe408a90f5e4af5ed2379bea40ced778b'>
  <p>
    This is a follow-up on my <a href="http://protocol7.com/archives/2007/11/28/easier-certificates-for-mq/">previous post on creating certificates for WebSphere MQ</a>.
  </p>
  
  <p>
    In one of my customers environment we began having troubles connecting to SSL secured WMQ channels as we upgraded the WebSphere Message Broker Toolkit to version 6.1. After opening a ticket with IBM and getting quite a few groups within Big Blue involved, it turned out that starting with the IBM Java 1.5 JRE, they have added a validation on Basic Constraints for CA certificates. WMB 6.1 ships with Java 1.5. The scripts I published in my last post does not set this attribute. As far as I&#8217;ve been able to find, there is no workaround besides recreating your CA certificate, which means re-signing all your keys. This annoys me, but given that the requirement for setting the Basic Constraints has been in the RFC <a href="http://www.ietf.org/rfc/rfc3280.txt">since before dawn</a>, the blame is pretty much my own.
  </p>
  
  <blockquote>
    <p>
      4.2.1.10 Basic Constraints<br /> The basic constraints extension identifies whether the subject of the<br /> certificate is a CA and the maximum depth of valid certification<br /> paths that include this certificate.<br /> <br /> The cA boolean indicates whether the certified public key belongs to<br /> a CA. If the cA boolean is not asserted, then the keyCertSign bit in<br /> the key usage extension MUST NOT be asserted.<br /> <br /> This extension MUST appear as a critical extension in all CA<br /> certificates that contain public keys used to validate digital<br /> signatures on certificates.
    </p>
  </blockquote>
  
  <p>
    Anyways, <a href="http://wmq-util.googlecode.com/svn/ssl-scripts/create-ca.sh">the script</a> is now updated. <a href="http://code.google.com/p/wmq-util/source/diff?r=31&#038;format=side&#038;path=/ssl-scripts/create-ca.sh">The required change</a> is to add the argument -ca true when creating the CA certificate.<br /> If you have any further suggestions to improve the scripts, please contact me and I&#8217;ll make sure to upgrade them.
  </p>
</div>
