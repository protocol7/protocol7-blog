---
id: 1587
title: last.fm does REST API, FAIL
date: 2008-06-29T06:55:08+00:00
author: Niklas
layout: post
guid: http://protocol7.com/?p=1587
permalink: /archives/2008/06/29/lastfm-does-rest-api-fail/
categories:
  - Uncategorized
tags:
  - last.fm
  - REST
---
<div class='microid-4d4acb7bc5caceeb471a28ef3df7884a275893fa'>
  <p>
    last.fm just <a href="http://blog.last.fm/2008/06/27/developers-developers-developers">launched their brand new API</a> (via <a href="http://sixx.se/nextgen/2008/06/28/lastfm-uppdaterar-sitt-api/">Fredrik</a>). Sporting support for both XML-RPC and REST. Now that&#8217;s a first sign of warning. And unsurprisingly it turns out that <a href="http://www.last.fm/api/rest">the &#8220;REST&#8221; API</a> is just another RPC over HTTP incarnation.
  </p>
  
  <blockquote>
    <p>
      For example.:
    </p>
    
    <pre><code>http://ws.audioscrobbler.com/2.0/?method=&lt;strong>artist.getSimilar&lt;/strong>&api_key=xxx...</code></pre>
    
    <p>
      If you are accessing a write service, you will need to submit your request as an HTTP POST request. All POST requests should be made to the root url:
    </p>
    
    <pre><code>http://ws.audioscrobbler.com/2.0/</code></pre>
  </blockquote>
  
  <p>
    WTF? Is it really that hard to get REST? To add insult to injury, they even <a href="http://www.last.fm/api/authspec">managed to make up their own authentication protocol</a>, despite, you know, OpenID and OAuth being <a href="http://googledataapis.blogspot.com/2008/06/oauth-for-google-data-apis.html">fairly mainstream</a> these days.
  </p>
</div>