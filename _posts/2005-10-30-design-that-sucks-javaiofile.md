---
id: 1084
title: 'Designs that sucks &#8211; java.io.File'
date: 2005-10-30T23:54:13+00:00
author: Niklas
layout: post
guid: http://www.protocol7.com/archives/2005/10/30/design-that-sucks-javaiofile/
permalink: /archives/2005/10/30/design-that-sucks-javaiofile/
tags:
  - Java
---
<div class='microid-bf7bce8915bad6546eb6f86917c71146b9490745'>
  <p>
    <a href="http://www.jroller.com/page/cpurdy/20051030">Cameron Purdy blogs on some of the more amazingly bad designs in Java</a>. While I certainly do not want to steal his thunder, I felt that I need to add my favorite offender to the list, java.io.File. What great minds got their heads together to come up with this crap? And what did they think? &#8220;Oh, we got this great C API for working with files, why use any of these new stuff we invented for Java&#8221;. So, what were we left with?
  </p>
  
  <p>
    Now, given that you have created your shiny File object, what would expect to be able to do? Create the actual file, well we got that almost covered. But, even though you have the exact same class for files, directories and links, you have to create them differently (and links, well you can&#8217;t create those at all) using createNewFile() or mkdir(). And what about that mkdirs(), method overloading anyone?
  </p>
  
  <p>
    That was great, now that we got our file, let&#8217;s move it should we. Okay, we got a renameTo() method that does that for us. But wait, what if the target already exists or we don&#8217;t have access to move it. Well, we get that useful false returned from the call. Why using those pesky exceptions when you can just return booleans instead?
  </p>
  
  <p>
    Alright, lets copy the file. No, that&#8217;s not supported. Some clever guy must have decided that copying files is such an rare use case that we shouldn&#8217;t waste one of those methods on that. What else? How about reading the file? Nope. Writing to it? Nope. Well, at least we got a few a pair of methods for deleting the file. <a href="http://blogs.codehaus.org/people/vmassol/archives/001036_id_love_reusable_ant_tasks.html">Only if it would work</a>.
  </p>
  
  <p>
    And, as Cameron points out, we got this great class for describing dates. How come get the the last modified time is served as a long? Or why is the getter for the last modified time named lastModified() instead of getLastModified() like the rest of the getters?
  </p>
  
  <p>
    Last but not least, we got the outstanding setReadOnly(). This little genious makes the file read-only. How about making the file writable again? Nope, obviously no one would ever need that.
  </p>
  
  <p>
    Lucky for us we got the blazingly fast people on <a href="http://www.jcp.org/en/jsr/detail?id=203">JSR 203</a> working for us.
  </p>
</div>