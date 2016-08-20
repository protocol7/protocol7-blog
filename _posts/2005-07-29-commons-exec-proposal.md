---
id: 1076
title: commons-exec proposal
date: 2005-07-29T18:32:42+00:00
author: Niklas
layout: post
guid: http://www.protocol7.com/archives/2005/07/29/commons-exec-proposal/
permalink: /archives/2005/07/29/commons-exec-proposal/
tags:
  - Java
---
<div class='microid-23751cfb8421f4e87d9ef494b0594bebfcd8f5e5'>
  <p>
    Posted to the Jakarta commons-dev mailing list. Feedback is very welcome!
  </p>
  
  <p>
    Proposal for Exec Package
  </p>
  
  <p>
    Rationale<br /> Executing external processes from Java is a well-known problem area. It is inheriently platform dependent and requires the developer to know and test for platform specific behaviors, for example using cmd.exe on Windows or limited buffer sizes causing deadlocks. The JRE support for this is very limited, albeit better with the new Java SE 1.5 ProcessBuilder class.
  </p>
  
  <p>
    Reliably executing external processes can also require knowledge of the environment variables before or after the command is executed. In J2SE 1.1-1.4 there is not support for this, since the method, System.getenv(), for retriving environment variables is deprecated.
  </p>
  
  <p>
    The are currently several different libraries that for their own purposes has implemented frameworks around Runtime.exec() to handle the various issue outlined above. The proposed project should aim at coordinating and learning from these initatives to create and maintain a simple, reusable and well-tested package. Since some of the more problematic platforms are not readily available, it is my hope that the broad Apache community can be a great help.
  </p>
  
  <p>
    Scope of the package<br /> <br /> The package shall create and maintain a process execution package written in the Java language to be distributed under the ASF license. The Java code might also be complemented with scripts (e.g. Perl scripts) to fully enable execution on some operating systems. The package should aim for supporting a wide range of operating systems while still having a consistent API for all platforms.
  </p>
  
  <p>
    Interaction with other packages<br /> <br /> This package will using Commons Logging for logging debug and error information.
  </p>
  
  <p>
    Identify the initial source for the package<br /> <br /> Several implementations exists and should be researched before finalizing the design:<br /> * Ant 1.X contains probably the most mature code within the exec task. This code has been stripped of the Ant specifics and cleaned up by Niklas Gustavsson and can be donated under the ASF license.<br /> * Ant 2.X contains a new exec implementation, especially targeted for reusability (see http://ant.apache.org/ant2/actionlist.html#exec).<br /> * plexus-utils has a similar but slimmer implementation than Ant and has also indicated interest through Trygve Laugstøl the particate in the development.
  </p>
  
  <p>
    Identify the base name for the package<br /> <br /> org.apache.commons.exec
  </p>
  
  <p>
    Identify the coding conventions for this package<br /> <br /> Sun conventions.
  </p>
  
  <p>
    Identify any Jakarta-Commons resources to be created<br /> <br /> * Mailing list<br /> Until traffic justifies, the package will use the Jakarta-Commons lists for communications.
  </p>
  
  <p>
    * SVN repositories<br /> A new SVN directory under Commons Sandbox
  </p>
  
  <p>
    * Bugzilla<br /> The package should be listed as a component of under the Jakarta-Commons Bugzilla entry.
  </p>
  
  <p>
    * Integration test builds<br /> If possible, some form of integration test builds on various platforms (like the SourceForge compile farm) would be invaluable. I'm unsure of what for example Gump and the current Apache infrastructure has to offer in this area.
  </p>
  
  <p>
    Identify the initial set of committers to be listed in the Status File<br /> <br /> Brett Porter<br /> Stefan Bodewig<br /> Niklas Gustavsson (I'm not currently an Apache commiter so I don't know if this is possible)
  </p>
</div>
