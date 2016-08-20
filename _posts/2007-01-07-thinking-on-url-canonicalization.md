---
id: 1409
title: Thinking on URL canonicalization
date: 2007-01-07T23:35:24+00:00
author: Niklas
layout: post
guid: http://protocol7.com/archives/2007/01/07/thinking-on-url-canonicalization/
permalink: /archives/2007/01/07/thinking-on-url-canonicalization/
tags:
  - Web
openid_comments:
  - 'a:1:{i:0;s:5:"23774";}'
categories:
  - REST
---
<div class='microid-7e24a8165d872bfe24ce2cfc3e9a837b7549b7f3'>
  <p>
    Over at REST-discuss there&#8217;s an interesting discussion going on regarding how to construct you URLs in the best way. <a href="http://www.artima.com/consulting.html">Bill Venners</a> of <a href="http://www.artima.com">Artima</a> posted a <a href="http://permalink.gmane.org/gmane.comp.web.services.rest/4646">very interesting note</a> on how he canonicalize all URLs, including the ordering of query parameters and removing default parameters, using redirects. His motivation for doing this, which I think is brilliant, is to <a href="http://permalink.gmane.org/gmane.comp.web.services.rest/4672">aid search engines in identifying two URLs as pointing to the same resource</a>. That is, if <a href="http://example.com/foo?a=1&b=2">http://example.com/foo?a=1&b=2</a> is his canonical URL, the following examples (with c having the default value of 3) would all get a 301 response pointing to the canonical URL above:
  </p>
  
  <ul>
    <li>
      <a href="http://example.com/foo?b=2&a=1">http://example.com/foo?b=2&a=1</a>
    </li>
    <li>
      <a href="http://example.com/foo?a=1&b=2&c=3">http://example.com/foo?a=1&b=2&c=3</a>
    </li>
    <li>
      <a href="http://example.com/foo?a=1&b=2%20">http://example.com/foo?a=1&b=2%20</a>
    </li>
  </ul>
  
  <p>
    Getting a search engine to figure out that all these are the same thing, would add up the four page rankings and likely make the final page a higher hit. Now, we don&#8217;t know how search engines do there rankings (or canonicalizations for that matter) but I think it&#8217;s a fair guess that this method helps along.
  </p>
  
  <p>
    In a response, Roy Fielding suggest he should use a canonical URL that doesn&#8217;t use query parameters at all, probably helping caches to do a better job. I think that makes sense as well, so these suggestions will now form my embryo for a URL c14n best practice:
  </p>
  
  <ol>
    <li>
      Don&#8217;t use query parameters in the URL of the final resource (a search result page is a different matter, but the actual final page should have a clean URL)
    </li>
    <li>
      Redirect cases where you need to use query parameters (e.g. when allowing a user to select a resource using&nbsp;for example an HTML form)&nbsp;to the canonical URL.
    </li>
    <li>
      When you really need a page identified by the query parameters (e.g. a search result page), redirect so that ordering and presence of&nbsp;query parameters are canonicalized
    </li>
  </ol>
</div>