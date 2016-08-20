---
id: 1663
title: Introducing Apache Vysper
date: 2011-01-09T23:04:27+00:00
author: Niklas
layout: post
guid: http://protocol7.com/?p=1663
permalink: /archives/2011/01/09/introducing-apache-vysper/
openid_comments:
  - 'a:3:{i:0;s:6:"128440";i:1;s:6:"132578";i:2;s:6:"132587";}'
categories:
  - Uncategorized
tags:
  - Apache
  - Jabber
  - vysper
  - XMPP
---
<div class='microid-a2349e9f392363ac85789fb65904234ff10f2b76'>
  <p>
    <img src="http://mina.apache.org/vysper/index.data/vysper_logo.png" alt="Vysper logo" style="float:right" /> This is the first in a series of posts I&#8217;m planning to do on <a href="http://mina.apache.org/vysper/">Apache Vysper</a>. This first post will mostly deal with what Vysper is, later posts will go into details on various ways of using Vysper.
  </p>
  
  <p>
    Vysper is an implementation of an <a href="http://en.wikipedia.org/wiki/Extensible_Messaging_and_Presence_Protocol">XMPP</a> (aka Jabber) server in Java. Vysper is a subproject of Apache MINA and is licensed under Apache License, Version 2.0. Vysper aims to run both standalone as well as embedded into your application. When running embedded, you can closely integrate your application with Vysper, e.g. to share user management or session state. Vysper is still in the early stages, but is certainly usable for early adopters. The currently released version is 0.6, but the example below is based on <a href="http://svn.apache.org/repos/asf/mina/vysper/trunk/">SVN trunk</a>, which will in the near future become 0.7.
  </p>
  
  <p>
    XMPP is specified as two RFCs (<a href="http://www.ietf.org/rfc/rfc3920.txt">RFC 3920</a>, <a href="http://www.ietf.org/rfc/rfc3921.txt">RFC 3921</a> for the core protocol and <a href="http://xmpp.org/extensions/">a great number of extensions, called XEP:s</a>. Vysper implements the RFCs as part of it&#8217;s server core. For many of the extensions, these are implemented as Vysper modules, meaning as a user, you can choose which modules to have run on your server. For example, some might want to use the <a href="http://xmpp.org/extensions/xep-0060.html">publish-subscribe extension</a> while others want to use the <a href="http://xmpp.org/extensions/xep-0045.html">multi-user chat</a> and <a href="http://xmpp.org/extensions/xep-0133.html">service administration</a> modules. XMPP also supports different network protocols, e.g. the main XML-over-TCP/IP protocol, HTTP long-polling (in XMPP-land called <a href="http://xmpp.org/extensions/xep-0206.html">BOSH</a>) or <a href="http://tools.ietf.org/html/draft-moffitt-xmpp-over-websocket-00">websockets</a>. Vysper implements these as so called Endpoints. And as with modules, the user can pick and choose which protocols are desired.
  </p>
  
  <p>
    For the exact details of which specifications Vysper support, please check this <a href="http://mina.apache.org/vysper/standards-support.html">link</a>.
  </p>
  
  <p>
    Configuring Vysper can either be done using the Java API as in the example below, or by using a dependency injection framework. Vysper currently ships with examples for Spring.
  </p>
  
  <p>
    Enough theory, let&#8217;s look at an example. The code below shows the basics of running Vysper from a simple Java application. Afterwards, we&#8217;ll look into what the code actually does.
  </p>
  
  <p>
    To get going, you need to download Vysper, in this case from SVN and build it using Maven (these instructions will be updated when Vysper 0.7 is released). The code below will work on 0.6 with some slight modifications. If building from source sounds intimidating, I&#8217;ve set up this example as <a href="https://github.com/protocol7/vysper-intro">a project on Github</a>, where you can also find archive downloads of the sample with the required dependencies.
  </p>
  
  <pre name="code" class="java">

 XMPPServer server = new XMPPServer("vysper.org");
        
 StorageProviderRegistry providerRegistry = new MemoryStorageProviderRegistry();

 AccountManagement accountManagement = (AccountManagement) providerRegistry.retrieve(AccountManagement.class);

 Entity user = EntityImpl.parseUnchecked("user@vysper.org");
 accountManagement.addUser(user, "password");

 server.setStorageProviderRegistry(providerRegistry);

 server.addEndpoint(new TCPEndpoint());

 server.setTLSCertificateInfo(new File("keystore.jks"), "sekrit");

 server.start();
 System.out.println("Vysper server is running...");

 server.addModule(new EntityTimeModule());
 server.addModule(new VcardTempModule());
 server.addModule(new XmppPingModule());
 server.addModule(new PrivateDataModule());
</pre>
  
  <p>
    Number below refer to code lines in the example above.<br /> 1. Create the server and provide the domain it will be running on. Users at this domain will be addressed as &#8220;foo@vysper.org&#8221;.<br /> 3. Create a storage provide registry. This is a service locator for all the different pieces in Vysper which needs to persist stuff, like users or rosters (the list of friends). In this case, we use the simplest implementation, which stores things in memory.<br /> 5-8. From the above service locator, get the storage provider for users in order to add a user for testing. XMPP uses user identifiers in the form username@domain, similar to mail. These are called entities. Here, you can probably imaging AccountManagement instead being an implementation which looks up users in LDAP or similar.<br /> 10. Set the storage provide registry on the server.<br /> 12. As described above, Vysper uses different types of endpoints for the different network protocols. TCPEndpoint implements the core XMPP protocol as described in RFC 3920. It&#8217;s required for regular XMPP clients like Adium or Psi to be able to connect to the server. By default, this uses port 5222.<br /> 14. Provide a PKI keystore, this enables the server to use SSL when clients connect and ensures that sensitive stuff (passwords as well as conversations) is kept secret.<br /> 16. Start the server. Vysper is now running and clients will be able to connect to it. You can try it out with your favourite IM client.<br /> 19-22. Here we add modules for some XMPP extensions. Which to use depends largely on the purpose of the server. These must be added after the server is started as they require the server to be fully initiated.
  </p>
  
  <p>
    And, that&#8217;s it. You now hopefully got a working XMPP server running and you can go play with the other neat features it supports. Also, if you have any further questions, feel free to ask on <a href="http://mina.apache.org/vysper/mailing-lists.html">our mailing list</a> or comment below.
  </p>
  
  <p>
    In the next post, I will describe the architecture of Vysper and how messages, called stanzas in XMPP terms, flow through the server.
  </p>
</div>