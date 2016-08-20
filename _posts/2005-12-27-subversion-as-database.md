---
id: 1099
title: Subversion as database
date: 2005-12-27T03:28:18+00:00
author: Niklas
layout: post
guid: http://www.protocol7.com/archives/2005/12/27/subversion-as-database/
permalink: /archives/2005/12/27/subversion-as-database/
tags:
  - Applications
---
<div class='microid-46839f5d247cd75ca31b2f0474f7ae23869ff220'>
  <p>
    After being a heavy subversion user for the last year or more I&#8217;m inclined to declare it the perfect tool for storing versioned documents. Of all types of SCMs (e.g CVS, VSS) and document handling systems (e.g. Documentum) I&#8217;ve worked with, SVN is the clear winner due it is very straightforward nature (it&#8217;s simply a versioned file system) and simple API (RESTish). Excellent clients like <a href="http://tortoisesvn.tigris.org/">TortoiseSVN</a> and <a href="http://subclipse.tigris.org/">Subclipse</a> doesn&#8217;t hurt either. Of course, it doesn&#8217;t do everything every other system does, especially when compared to the high-end document handlers like Documentu. But then on the other hand, who really needs that functionality? Mostly you just want a safe way of storing your documents in a way where you can browse, retrive, change, revert and possibly audit them. And subversion fits those use cases significantly better than any other tool I have any experience with.
  </p>
  
  <p>
    Now, to stretch this a bit further I was thinking of other systems where using subversion as storage might be useful. Especially in systems where you handle versioned document-type data. Two types of applications seems obvious to me: wikis and blogs. In both of these, the primary data is a clob with some metadata (like author and a publishing timestamp). In wikis especially, versioning is crucial due to the nature of multiple, possibly anonymous (or spamming) authors. I bet that basing a wiki around subversion instead of inventing your own RDMS based revision system will be significantly easier and require less coding. And with the native libraries for the popular programming languages (e.g. <a href="http://tmate.org/svn/">Java</a>, <a href="http://www.cs.toronto.edu/%7Ejames/svn/ruby_docs.html">Ruby</a>, .<a href="http://www.softec.st/ClrProjects/wiki/SubversionSharp">NET</a>, <a href="http://pysvn.tigris.org/">Python</a>), this is bound to get even easier.
  </p>
  
  <p>
    I can see one obvious issue, scalability. Subversion is built for a limited number of concurrent users, not what would be expected from a popular wiki or blog. This is an area where the traditional databases excel. However, for cases where you have more readers than writers (as would be expected for a blog or wiki), this can be solved using caching.
  </p>
  
  <p>
    As an additional bonus, for applications using their wiki as the main documentation (like <a href="http://opensource2.atlassian.com/confluence/oss/pages/viewpage.action?pageId=1692">Geronimo</a>), you could cut releases of the online documentation in the same way as you do with the rest of your artifacts, simply by tagging. It would also be easy to incorporate in your standard build process, for example with a wiki storing the text as APT (or other foramts as markdown) you could use Maven to tag, compile your code and build a PDF for the documentation using nothing more than the standard Maven plugins.
  </p>
  
  <p>
    Does anyone know of any application built this way? I would be very interested in <a href="mailto:niklas@protocol7.com">feedback</a> on these ideas.
  </p>
</div>