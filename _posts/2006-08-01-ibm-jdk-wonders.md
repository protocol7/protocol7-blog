---
id: 1268
title: IBM JDK wonders
date: 2006-08-01T23:19:00+00:00
author: Niklas
layout: post
guid: http://www.protocol7.com/archives/2006/08/01/ibm-jdk-wonders/
permalink: /archives/2006/08/01/ibm-jdk-wonders/
tags:
  - Java
  - Testing
  - Zystems
---
<div class='microid-ba0f9890c9e172ee5fa3f39f28c27483578fe381'>
  <p>
    Last week I had the joy of setting up our <a href="http://zutubi.com/products/pulse/">new build server</a> at <a href="http://www.zystems.se">work</a>. Since we deal with integrating with legacy applications on god-forbidden platforms, we still need to support JDK 1.3. Since some of these platforms are somewhat weird, this tends to mean IBM JDK 1.3. But we&#8217;ve been sloppy with building on this JDK for some of our projects. Now, when setting up the build server I made sure to include both IBM JDK 1.3 and 1.4 in the available options and also included them for our main projects. They all broke. Not because we were using some fancy stuff in 1.4. No, no, they broke with the wonderful error<br /> 
    
    <blockquote>
      <pre>error: The encoding null is not supported</pre>
    </blockquote>
    
    <p>
      Google to the rescue, finds <a href="http://www.bright-green.com/blog/2003_09_22/why_i_drink_coffee.html">this page</a>. Turns out that this train-wreck of a JDK doesn&#8217;t support non-ASCII characters in the Java source files. Since we&#8217;re a Swedish company, quite a few people has included @author tags which contains the letters &aring;&auml;&ouml;. Lots of search-and-replaces later all of those has been replaced with the harmless a and o. Oh, and someone also made the mistake of including some curly quotes in a comment which had to be replaced.&nbsp; That was boring, but easy. A lot of builds still wouldn&#8217;t work. That&#8217;s because some of the i18n unit tests contains strings with funky characters. Had to replace with loading that text from a file. Now everything worked as expected.
    </p>
    
    <p>
      Only that some build should instead run on IBM JDK 1.4. These instead produce the equally wonderful<br /> 
      
      <blockquote>
        <pre>error: IO exception sun.io.MalformedInputException</pre>
      </blockquote>
      
      <p>
        Gee, thanks. Very helpful this time too. Google again. Found <a href="http://lists.terrasoftsolutions.com/pipermail/yellowdog-general/2005-January/017518.html">this page</a>. This time I had to set the LANG environment variable to make the system not using UTF-8 (which Ubuntu does by default). Luckily, Pulse made this very easy.
      </p>
      
      <p>
        Finally all builds worked, a few hours of massaging perfectly fine projects to build on buggy JDKs. An this was still on Linux, not one of the weird platforms. Luckily, JDKs tends to get better with each new version.
      </p></div>
