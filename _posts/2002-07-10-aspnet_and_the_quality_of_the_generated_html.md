---
id: 589
title: ASP.NET and the quality of the generated HTML
date: 2002-07-10T12:25:31+00:00
author: Niklas
layout: post
guid: http://www.protocol7.com/archives/2002/07/10/aspnet-and-the-quality-of-the-generated-html/
permalink: /archives/2002/07/10/aspnet_and_the_quality_of_the_generated_html/
tags:
  - HTML/XHTML
---
<div class='microid-1fd2f8cc9c27b5a1e5e31d609beaf1bd2a5c58f3'>
  <p>
    Been playing some with the ASP.NET web forms in Visual Studio.NET lately and I find the quality of the HTML generated from them terrible. I would expect it to, at least, produce valid XHTML (without breaking IE 5.0 support). It just seems that Microsoft were sloppy when building the HTML generator. For example, why are some empty tags closed and some are not?
  </p>
  
  <p>
    And I don&#8217;t think that, for example:
  </p>
  
  <ul>
    <li>
      use a doctype that triggers standards compliance mode in IE6
    </li>
    <li>
      use consistent lower-case styles
    </li>
    <li>
      not sticking MS specific attributes (that not even IE uses) on tags
    </li>
    <li>
      automatically putting all styles in a CSS instead of inline
    </li>
  </ul>
  
  <p>
    are to much to ask for.
  </p>
  
  <p>
    If anyone is working on subclassing the web forms to produce better output or have another solution, please <a href="mailto:niklas@protocol7.com">tell me</a> and I might actually find web forms okay to use some day :-)
  </p>
</div>