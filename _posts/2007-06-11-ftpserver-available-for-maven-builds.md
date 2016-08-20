---
id: 1510
title: FtpServer available for Maven builds
date: 2007-06-11T22:52:10+00:00
author: Niklas
layout: post
guid: http://protocol7.com/archives/2007/06/11/ftpserver-available-for-maven-builds/
permalink: /archives/2007/06/11/ftpserver-available-for-maven-builds/
tags:
  - Apache
  - FtpServer
  - Open source
---
<div class='microid-e0e24e2dafd414f76aea7235c43f5bee6a8b48ee'>
  <p>
    Starting today, <a href="http://incubator.apache.org/ftpserver/">Apache Incubator FtpServer</a> JARs are <a href="http://people.apache.org/maven-snapshot-repository/org/apache/ftpserver/">available</a> from the <a href="http://people.apache.org/maven-snapshot-repository/">Apache snapshot repository</a>. This should make it easy to use FtpServer in your Maven 2 build. Just declare the following dependency and you&#8217;re done.
  </p>
  
  <p>
    <code>
&lt;pre>
    &lt;dependency&gt;
      &lt;groupId&gt;org.apache.ftpserver&lt;/groupId&gt;
      &lt;artifactId&gt;ftpserver-core&lt;/artifactId&gt;
      &lt;version&gt;1.0-incubator-SNAPSHOT&lt;/version&gt;
    &lt;/dependency&gt;
&lt;/pre>
&lt;p></code>
  </p>
  
  <p>
    Currently, the snapshots will be deployed manually, but I&#8217;m working on getting a CI build up and running that would also deploy snapshots automagically.
  </p>
</div>