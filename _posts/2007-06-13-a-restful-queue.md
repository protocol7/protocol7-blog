---
id: 1513
title: A RESTful queue
date: 2007-06-13T22:36:56+00:00
author: Niklas
layout: post
guid: http://protocol7.com/archives/2007/06/13/a-restful-queue/
permalink: /archives/2007/06/13/a-restful-queue/
tags:
  - Messaging/JMS
categories:
  - REST
---
<div class='microid-6c5f3d2fcc74e7a388adf7dce3c4f7e66aa8687c'>
  <p>
    As messaging and therefore queues is close to my heart, I&#8217;ve been following the <a href="http://permalink.gmane.org/gmane.comp.web.services.rest/6149">discussions on rest-discuss</a> on how to construct a RESTful queue with great interest. The discussion started (as did my thinking on the topic a year or so back) around how ActiveMQ has choosen to implement <a href="http://activemq.apache.org/rest.html">their REST support</a>, a somewhat broken model as pointed out by Paul Winkler (e.g. non-safe GET, DELETE on queue deletes message rather than the queue).
  </p>
  
  <p>
    My favorite model so far is <a href="http://permalink.gmane.org/gmane.comp.web.services.rest/6186">the one suggested by Steve Bjorg</a>, also quite similar to the <a href="http://www.dehora.net/doc/httplr/draft-httplr-01.html#rfc.section.9">one described in HTTPLR</a>. In that case you would push messages onto a queue with POST and pop then with a combination of POST and DELETE. To quote from Steve&#8217;s email.<br /> 
    
    <blockquote>
      To add an item:<br />POST /queue<br />Content-Type: application/xml (or whatever a queue item is)<br />&#8211;><br />201 Created<br />Location: http://server.com/queue/itemXYZ</p> 
      
      <p>
        To request to pop an item:<br />POST /queue<br />Content-Type: application/w-www-form-urlencoded<br />AckTTL=60 (where AckTTL is the time to acknowledge the queue item or<br />it becomes available again)<br />&#8211;><br />200 Ok<br />http://server.com/queue/itemABC
      </p>
      
      <p>
        To delete a popped item:<br />DELETE /queue/itemABC<br />&#8230;
      </p>
    </blockquote>
    
    <p>
      Go read the discussion thread as it contains many interesting aspects on this pretty hard problem. Ideas on how to improve the current suggestions is very welcome.
    </p></div>