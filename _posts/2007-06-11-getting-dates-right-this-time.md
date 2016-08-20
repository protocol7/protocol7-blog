---
id: 1511
title: Getting dates right this time
date: 2007-06-11T23:12:34+00:00
author: Niklas
layout: post
guid: http://protocol7.com/archives/2007/06/11/getting-dates-right-this-time/
permalink: /archives/2007/06/11/getting-dates-right-this-time/
tags:
  - Java
---
<div class='microid-a1dc797c0b399b641be44cef11fa68286e0d1b88'>
  <p>
    There&#8217;s tons of interesting discussions going on the the <a href="https://jsr-310.dev.java.net/servlets/SummarizeList?listName=dev">JSR-310 dev list</a> right now. It&#8217;s the JSR for developing the <a href="https://jsr-310.dev.java.net/">new(er) date and time API for Java</a>, based of <a href="http://joda-time.sourceforge.net">Joda Time</a>. The discussions are currently covering two important aspects, the basic design principles for the API and how to handle <a href="https://jsr-310.dev.java.net/servlets/ReadMsg?list=dev&msgNo=462">non-Gregorian calendars</a>. The latter being something that the Calendar API failed at miserably. Not that it didn&#8217;t support it correctly, just that it did it in such an intrusive way that you quickly get annoyed with it.
  </p>
  
  <p>
    The design principles this far looks well thought out:
  </p>
  
  <ol>
    <li>
      <a href="https://jsr-310.dev.java.net/servlets/ReadMsg?list=dev&msgNo=413">Immutable</a>
    </li>
    <li>
      <a href="https://jsr-310.dev.java.net/servlets/ReadMsg?list=dev&msgNo=414">Fluent API</a>
    </li>
    <li>
      <a href="https://jsr-310.dev.java.net/servlets/ReadMsg?list=dev&msgNo=423">Clear, explicit and expected</a>
    </li>
  </ol>
  
  <p>
    I think that setting basic principles like this for your API is a really good idea. As we learn more and more on what the winning principles are, it would be a topic for a book to collect them much like the GoF book. Personally, I think the <a href="http://www.xom.nu/designprinciples.xhtml">XOM principles</a> (also <a href="http://www.artima.com/weblogs/viewpost.jsp?thread=142428">covered here</a>) are the best general guideline currently available.
  </p>
</div>