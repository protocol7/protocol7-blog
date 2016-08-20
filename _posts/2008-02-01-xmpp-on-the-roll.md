---
id: 1556
title: XMPP on the roll
date: 2008-02-01T15:36:40+00:00
author: Niklas
layout: post
guid: http://protocol7.com/archives/2008/02/01/xmpp-on-the-roll/
permalink: /archives/2008/02/01/xmpp-on-the-roll/
tags:
  - Jabber
  - OSGi
  - XMPP
---
<div class='microid-17ef5599a054bbcbdca72ccf1893ec71f33bf1d4'>
  <p>
    I first wrote this quick introduction to XMPP for <a href="http://wiki.callistaenterprise.se/display/CallistaCom/2008/02/01/XMPP+on+the+roll">our blog at work</a>, I&#8217;m publishing this copy over here to keep my useful posts in one place. Expect to find more posts on OSGi and XMPP here in the future.
  </p>
  
  <p>
    <a href="http://www.xmpp.org/">XMPP</a>, aka Jabber, is making great strides into the world of instant messaging. Since <a href="http://www.jeremie.com/blog/">Jeremie Miller</a> released the first version in 1998, it has been the obvious alternative for those preferring open protocols over the proprietary networks pushed by ICQ, AOL, MSN and others. With big guys like <a href="http://www.apple.com/se/server/macosx/features/ichat.html">Apple</a> and <a href="http://code.google.com/apis/talk/open_communications.html">Google</a> using XMPP it began making noise in the corporate world. Now, with AOL (one of the biggest IM network provider) <a href="http://florianjensen.com/2008/01/17/aol-adopting-xmpp-aka-jabber/">looking at XMPP</a>, the road to world dominance seems clear ahead.
  </p>
  
  <p>
    So what&#8217;s in it for us, the application developers? One example is keeping an eye on our applications. XMPP provides two perfectly fitting concepts:<br /> * Presence &#8211; what modules are up and running<br /> * Messages &#8211; communicate with your application
  </p>
  
  <p>
    Let&#8217;s have a look at a simple example. Note this is a demo code, quality code might use things like clever things like exception handling and external configuration. But for now, this will do.
  </p>
  
  <p>
    First of all, you need two Jabber/GTalk accounts. Go <a href="http://www.jabber.org/user/userguide/#register">create them</a> (if you don&#8217;t already have a few), make sure they are buddies and get back here&#8230; back already? That was fast.
  </p>
  
  <p>
    Now, let&#8217;s write a simple <a href="http://www.osgi.org/">OSGi</a> bundle that sends its presence based on the state in its life cycle. Feel free to imagining how this would work with Spring or EJB life cycle if that&#8217;s tickles you more. OSGi has what is called a <a href="http://www2.osgi.org/javadoc/r4/org/osgi/framework/BundleActivator.html">BundleActivator</a> that keeps track of when a bundle is started and stopped (that&#8217;s InitializingBean and DisposableBean for all of you in Spring land). Let&#8217;s create an implementation.
  </p>
  
  <pre>
import org.osgi.framework.BundleActivator;
import org.osgi.framework.BundleContext;

public class Activator implements BundleActivator {

	@Override
	public void start(BundleContext context) throws Exception {

	}

	@Override
	public void stop(BundleContext context) throws Exception {

	}
}
</pre>
  
  <p>
    Choose one of many XMPP clients available in Java. One of the easier is the <a href="http://www.igniterealtime.org/projects/smack/index.jsp">Smack client</a> from Jive^H^H^H^H Ignite Realtime, also available for <a href="http://www.mvnrepository.com/artifact/jivesoftware/smack">all your Maven needs</a>. Let&#8217;s create and connect one when our BundleActivator is created:
  </p>
  
  <pre>
import org.jivesoftware.smack.ConnectionConfiguration;
import org.jivesoftware.smack.XMPPConnection;
import org.jivesoftware.smack.XMPPException;
import org.jivesoftware.smack.packet.Message;
import org.osgi.framework.BundleActivator;
import org.osgi.framework.BundleContext;

public class Activator implements BundleActivator {

	private XMPPConnection conn;
	
	private String server 			= "jabber.org";
	private int port 			= 5222;
	private String userName 		= "myuser";
	private String password 		= "secret";
	private String receiver 		= "myotheruser@gmail.com";
	
	public Activator() throws XMPPException  {
		ConnectionConfiguration config = new ConnectionConfiguration(server, port);
		conn = new XMPPConnection(config);
	}
        
        ...
}

</pre>
  
  <p>
    I did tell you this is demo-quality code, right. If this were production code you would certainly want to inject that connection into your code rather than hard coding it. Fine, now, let&#8217;s show when the bundle goes active or is stopped by indicating our presence:
  </p>
  
  <pre>
import org.jivesoftware.smack.ConnectionConfiguration;
import org.jivesoftware.smack.XMPPConnection;
import org.jivesoftware.smack.XMPPException;
import org.jivesoftware.smack.packet.Message;
import org.jivesoftware.smack.packet.Presence;
import org.osgi.framework.BundleActivator;
import org.osgi.framework.BundleContext;

public class Activator implements BundleActivator {

	private static final Presence AVAILABLE = new Presence(Presence.Type.AVAILABLE);
	private static final Presence UNAVAILABLE = new Presence(Presence.Type.UNAVAILABLE);
	
        ...
	
	@Override
	public void start(BundleContext context) throws Exception {
		conn.login(userName, password);

		conn.sendPacket(AVAILABLE);
	}

	@Override
	public void stop(BundleContext context) throws Exception {
 		conn.sendPacket(UNAVAILABLE);
 		
 		conn.close();
	}
}
</pre>
  
  <p>
    We&#8217;re almost done. Why not get a message that tells us that the bundle has started and all is good. This is the complete code listing:
  </p>
  
  <pre>
import org.jivesoftware.smack.ConnectionConfiguration;
import org.jivesoftware.smack.XMPPConnection;
import org.jivesoftware.smack.XMPPException;
import org.jivesoftware.smack.packet.Message;
import org.jivesoftware.smack.packet.Presence;
import org.osgi.framework.BundleActivator;
import org.osgi.framework.BundleContext;

public class Activator implements BundleActivator {

	private static final Presence AVAILABLE = new Presence(Presence.Type.AVAILABLE);
	private static final Presence UNAVAILABLE = new Presence(Presence.Type.UNAVAILABLE);
	
	private XMPPConnection conn;
	
	private String server 			= "jabber.org";
	private int port 			= 5222;
	private String userName 		= "myuser";
	private String password 		= "secret";
	private String receiver 		= "myotheruser@gmail.com";
	
	public Activator() throws XMPPException  {
		ConnectionConfiguration config = new ConnectionConfiguration(server, port);
		conn = new XMPPConnection(config);
	}
	
	@Override
	public void start(BundleContext context) throws Exception {
		conn.login(userName, password);

		conn.sendPacket(AVAILABLE);
		
		Message msg = new Message(receiver);
		msg.setBody("Bundle " + context.getBundle().getSymbolicName() + " started");
		conn.sendPacket(msg);
	}

	@Override
	public void stop(BundleContext context) throws Exception {
		Message msg = new Message(receiver);
		msg.setBody("Bundle " + context.getBundle().getSymbolicName() + " stopped");
		conn.sendPacket(msg);
		
 		conn.sendPacket(UNAVAILABLE);
 		
 		conn.close();
	}
}
</pre>
  
  <p>
    We&#8217;re done with coding. An OSGi bundle requires some extra attributes in the manifest but I won&#8217;t describe them in any detail here, go read any of the <a href="http://www.google.se/search?q=osgi+tutorial">OSGi tutorials</a> or the <a href="http://www2.osgi.org/Download/Release4V40">surprisingly readable specification</a> if you want to understand them.
  </p>
  
  <pre>
Bundle-Version: 1.0
Bundle-SymbolicName: se.callistaenterprise.osgi.xmpp
Bundle-Name: XMPP-Bundle
Bundle-Vendor: Callista Enterprise
Bundle-ManifestVersion: 2
Bundle-Activator: se.callistaenterprise.osgi.xmpp.Activator
Import-Package: org.osgi.framework,javax.net.ssl
Bundle-ClassPath: .,lib/smack-2.2.1.jar
</pre>
  
  <p>
    Now package all of that into a JAR, including the Smack JAR, and fire up your favorite OSGi implementation. You do have a a favorite one, right?
  </p>
  
  <p>
    For me, that means the <a href="http://felix.apache.org/">Apache Felix</a> <a href="http://felix.apache.org/site/apache-felix-usage-documentation.html">shell</a>:
  </p>
  
  <pre>
$ java -jar bin/felix.jar

Welcome to Felix.
=================

Enter profile name: xmpp

DEBUG: WIRE: 1.0 -&gt; org.ungoverned.osgi.service.shell -&gt; 1.0
DEBUG: WIRE: 1.0 -&gt; org.osgi.service.startlevel -&gt; 0
DEBUG: WIRE: 1.0 -&gt; org.apache.felix.shell -&gt; 1.0
DEBUG: WIRE: 1.0 -&gt; org.osgi.framework -&gt; 0
DEBUG: WIRE: 1.0 -&gt; org.osgi.service.packageadmin -&gt; 0
DEBUG: WIRE: 2.0 -&gt; org.apache.felix.shell -&gt; 1.0
DEBUG: WIRE: 2.0 -&gt; org.osgi.framework -&gt; 0
DEBUG: WIRE: 3.0 -&gt; org.osgi.framework -&gt; 0
DEBUG: WIRE: 3.0 -&gt; org.osgi.service.obr -&gt; 3.0
DEBUG: WIRE: 3.0 -&gt; org.apache.felix.shell -&gt; 1.0
-&gt;                                                         
</pre>
  
  <p>
    Start the bundle by running &#8220;start 4&#8221; and you should see the Jabber user getting online and get a message saying that everything is okay. Stop it with &#8220;stop 4&#8221; and you should get a message and see it go offline. Imagining having that with all your components and not having to depend on that monitoring system or wading through log files.
  </p>
  
  <pre>
-&gt; install file:///path/to/project/xmpp-bundle-1.0.jar
Bundle ID: 4
-&gt; start 4
# Some error messages from Smack that you can happily ignore
-&gt; stop 4
</pre>
  
  <p>
    For all you OSGi geeks, have a go at wrapping this code into a service that all your bundles can use. That&#8217;s what I do.
  </p>
  
  <p>
    Seems useful? Got any ideas as to where you could use XMPP communicating with you?
  </p>
  
  <p>
    Technorati Tags: <a class="performancingtags" href="http://technorati.com/tag/xmpp" rel="tag">xmpp</a>, <a class="performancingtags" href="http://technorati.com/tag/osgi" rel="tag">osgi</a>, <a class="performancingtags" href="http://technorati.com/tag/im" rel="tag">im</a>, <a class="performancingtags" href="http://technorati.com/tag/java" rel="tag">java</a>
  </p>
</div>