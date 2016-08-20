---
id: 1276
title: How do you compile your releases?
date: 2006-08-09T23:14:40+00:00
author: Niklas
layout: post
guid: http://www.protocol7.com/archives/2006/08/09/how-do-you-compile-your-releases/
permalink: /archives/2006/08/09/how-do-you-compile-your-releases/
tags:
  - Java
---
<div class='microid-28d7d2c2a4950d37735e650a6f42174ce517e39f'>
  <p>
    When discussing our release builds at work today, I found <a href="http://www.javaworld.com/javaqa/2003-05/02-qa-0523-version-p3.html">this article</a> which got me thinking. The author argues that you want the latest javac for your compilations, something I agree with. There has been quite a few bugs in the compilers (see my <a href="http://www.protocol7.com/archives/2006/08/01/ibm-jdk-wonders/">earlier post on the IBM JDK 1.3 compiler&#8230;</a>) warranting using the latest and greatest. Also, since the feature set of javac haven&#8217;t changed that much, you would expect it to have continously improved over time (better test suites would also add to this).
  </p>
  
  <p>
    The -target parameter for javac will make it produce Java byte code of the right version. But, if you&#8217;re not targeting the latest class libraries, you certainly want to catch any problems with using new features (like the classic &#8220;new RuntimeException(cause)&#8221;) during compilation. Now, the author argues for using a new javac and replacing the boot class loader classpath with an old rt.jar.
  </p>
  
  <p>
    What do you think? How do you make your release builds? I will play around with the recommendations in the article just to see how it works out. Maven1 seems to support it using the undocumented maven.compile.bootclasspath property. Ant provides the bootclasspath for the <a href="http://ant.apache.org/manual/CoreTasks/javac.html">javac task</a>.
  </p>
</div>