---
id: 1252
title: Acegi Security System and Active Directory howto
date: 2006-07-16T18:24:10+00:00
author: Niklas
layout: post
guid: http://www.protocol7.com/archives/2006/07/16/acegi-security-system-and-active-directory-howto/
permalink: /archives/2006/07/16/acegi-security-system-and-active-directory-howto/
tags:
  - Java
  - Open source
  - Security
  - Spring
---
<div class='microid-8f7b2ad9b194a1ce2f657e487daa48b14056ded5'>
  <p>
    At work, I&#8217;m finishing up an application that uses <a href="http://acegisecurity.org">Acegi Security System</a> for authentication and authorization. Last week, I had to create an example configuration that used Active Directory for verifying users and assigning them roles that would allow them into the application. Now, this is probably pretty easy if you know Acegi and LDAP, but since I&#8217;m pretty poor at both of them it took me half a day. To save your time (should you be as ignorant as I am), here&#8217;s how I did it.
  </p>
  
  <p>
    I should point out that below I use Acegi as the name of Acegi Security System. This is not recommended but I though that it&#8217;s a least better then ASS ;-)
  </p>
  
  <p>
    To start with, my requirements was that I wanted to use the mail alias (in my case niklas.gustavsson) as the login name, not the CN. In our AD (and most others I presume) this is stored in the mailNickname attribute. If you like to use the sAMAccountName it will work the same way, just replace mailNickname.<br /> Second, I wanted users from three different groups (our three offices) to have access.
  </p>
  
  <p>
    The main Acegi file is pretty much the boilerplate config from the &#8220;Tutorial Sample&#8221; so I won&#8217;t go into very much depth on that here. What we need in addition to that files, is a working AuthenticationProvider that can be plugged in. For LDAP, there is LdapAuthenticationProvider. The provider needs two things, an Authenticator and an AuthoritiesPopulator.
  </p>
  
  <h3>
    The Authenticator
  </h3>
  
  <p>
    For authenticator there are two options, <span class="sect3" /><a href="http://acegisecurity.org/docbook/acegi.html#ldap-ldap-authenticators-bind">BindAuthenticator</a> that will try to bind (login) to the LDAP server as the user and <span class="sect3" /><a href="http://acegisecurity.org/docbook/acegi.html#ldap-ldap-authenticators-password">PasswordComparisonAuthenticator</a> that will use the LDAP compare function to verify the provided password with that stored in LDAP. I went for BindAuthenticator, can&#8217;t really say if this decision makes any difference but it worked for me.
  </p>
  
  <p>
    The BindAuthenticator needs the connection details for the LDAP server, provided by a Context, in Acegi a DefaultInitialDirContextFactory. Here you just provide the URL to your server (e.g. ldap://ad.example.com), the DN for the user you want to use for lookups, this needs to be a full DN, and the password for that user. In their example, Acegi includes a BaseDN in the server URL, this did not work for me and my config only started working after removing it.
  </p>
  
  <p>
    <code>&lt;br />
&lt;bean id="initialDirContextFactory"&lt;br />
class="org.acegisecurity.ldap.DefaultInitialDirContextFactory"&gt;&lt;br />
&lt;constructor-arg value="ldap://ad.example.com"/&gt;&lt;br />
&lt;property name="managerDn"&gt;&lt;br />
&lt;value&gt;CN=queryuser,CN=Users,DC=example,DC=com&lt;/value&gt;&lt;br />
&lt;/property&gt;&lt;br />
&lt;property name="managerPassword"&gt;&lt;br />
&lt;value&gt;secret&lt;/value&gt;&lt;br />
&lt;/property&gt;&lt;br />
&lt;/bean&gt;&lt;br />
</code>
  </p>
  
  <p>
    Now, here comes the first tricky part. The example in the Acegi documentation uses the userDnPatterns property on BindAuthenticator to perform the bind. Now, I was only able to get this working when logging in using my CN (Niklas Gustavsson) but since I wanted to use the mailNickname I was stuck here. Instead I had to use the filter search capabilities (did I say that Acegi is a marvel of flexibility with the price of complexity?). Here is my understanding of how this works.
  </p>
  
  <ol>
    <li>
      Instead of binding directly, Acegi uses the filter to find a matching user
    </li>
    <li>
      If no user is found, that&#8217;s a failure.
    </li>
    <li>
      If a user is found, takes that users DN and tries to bind using it
    </li>
    <li>
      Success to bind means that we are okay, failure means incorrect password
    </li>
  </ol>
  
  <p>
    So, we need to set up a filter search. This is done using a FilterBasedLdapUserSearch with the following constructor arguments:
  </p>
  
  <ul>
    <li>
      The BaseDN for the search, for example OU=Users,DC=example,DC=com
    </li>
    <li>
      The filter statement
    </li>
    <li>
      The context factory
    </li>
  </ul>
  
  <p>
    I also provided a property to enable search on any sublevel, leaving the following configuration:<br /> <code>&lt;br />
&lt;bean id="userSearch" class="org.acegisecurity.ldap.search.FilterBasedLdapUserSearch"&gt;&lt;br />
&lt;constructor-arg index="0"&gt;&lt;br />
&lt;value&gt;OU=Users,DC=example,DC=com&lt;/value&gt;&lt;br />
&lt;/constructor-arg&gt;&lt;br />
&lt;constructor-arg index="1"&gt;&lt;br />
&lt;value&gt;(mailNickname={0})&lt;/value&gt;&lt;br />
&lt;/constructor-arg&gt;&lt;br />
&lt;constructor-arg index="2"&gt;&lt;br />
&lt;ref local="initialDirContextFactory"/&gt;&lt;br />
&lt;/constructor-arg&gt;&lt;br />
&lt;property name="searchSubtree"&gt;&lt;br />
&lt;value&gt;true&lt;/value&gt;&lt;br />
&lt;/property&gt;&lt;br />
&lt;/bean&gt;&lt;br />
</code>
  </p>
  
  <p>
    Now we&#8217;re ready to wire up the BindAuthenticator providing the context factory as a constructor argument and the filter search as the userSearch property:<br /> <code>&lt;br />
&lt;bean class="org.acegisecurity.providers.ldap.authenticator.BindAuthenticator"&gt;&lt;br />
&lt;constructor-arg&gt;&lt;br />
&lt;ref local="initialDirContextFactory"/&gt;&lt;br />
&lt;/constructor-arg&gt;&lt;br />
&lt;property name="userSearch" ref="userSearch"/&gt;&lt;br />
&lt;/bean&gt;&lt;br />
</code>
  </p>
  
  <h3>
    The AuthoritiesPopulator
  </h3>
  
  <p>
    Now, with the user authenticated we need to assign it a role that will allow access to the application. The simplest way to do this is with the DefaultLdapAuthoritiesPopulator. This class will populate the user with a set of roles based on the groups of which its a member. By default it will prefix the role name with &#8220;ROLE_&#8221; and uppercase the group name. So, a user which is a member of &#8220;MyAppUsers&#8221; and &#8220;MyAppAdmins&#8221; will get the roles ROLE_MYAPPUSERS and ROLE_MYAPPADMINS. Good enough, but how do we configure the populator? First we need the BaseDN for groups (e.g. CN=GroupsDC=example,DC=com) and second the attribute that you want to use for the role name, in our case &#8220;cn&#8221;. The configuration would then look like this:<br /> <code>&lt;br />
&lt;bean class="org.acegisecurity.providers.ldap.populator.DefaultLdapAuthoritiesPopulator"&gt;&lt;br />
&lt;constructor-arg&gt;&lt;br />
&lt;ref local="initialDirContextFactory"/&gt;&lt;br />
&lt;/constructor-arg&gt;&lt;br />
&lt;constructor-arg&gt;&lt;br />
&lt;value&gt;CN=Groups,DC=example,DC=com&lt;/value&gt;&lt;br />
&lt;/constructor-arg&gt;&lt;br />
&lt;property name="groupRoleAttribute"&gt;&lt;br />
&lt;value&gt;cn&lt;/value&gt;&lt;br />
&lt;/property&gt;&lt;br />
&lt;/bean&gt;&lt;br />
</code>
  </p>
  
  <p>
    What will happen is that Acegi will search this BaseDN for groups of which our user is listed in the &#8220;member&#8221; attribute. After that, it will take the CN of those groups, prefix, uppercase and assign as roles to the authenticated user.
  </p>
  
  <p>
    Now all you need to do is to configure a LdapAuthenticationProvider with the BindAuthenticator as the first constructor argument and the DefaultLdapAuthoritiesPopulator as the last.
  </p>
  
  <p>
    The full example configuration can be downloaded <a href="http://protocol7.com/code/acegi-ldap/applicationContext-acegi-security-ldap.xml">here</a>.
  </p>
  
  <h3>
    The objectDefinitionSource
  </h3>
  
  <p>
    Last but not least, we need to configure the objectDefinitionSource in the boilerplate file from the tutorial sample to allow users with the correct roles to log in.
  </p>
  
  <p>
    <code>&lt;br />
&lt;property name="objectDefinitionSource"&gt;&lt;br />
&lt;value&gt;&lt;br />
CONVERT_URL_TO_LOWERCASE_BEFORE_COMPARISON&lt;br />
PATTERN_TYPE_APACHE_ANT&lt;br />
/login=IS_AUTHENTICATED_ANONYMOUSLY&lt;br />
/**=ROLE_MYAPPUSERS&lt;br />
&lt;/value&gt;&lt;br />
&lt;/property&gt;&lt;br />
</code>
  </p>
  
  <p>
    Here we set the role ROLE_MYAPPUSERS should be allowed to access any URL of the application. We make one exception for the login page which any (unauthenticated) user can access, otherwise it would be impossible to log in.
  </p>
  
  <h3>
    Summary
  </h3>
  
  <p>
    That&#8217;s all you need to talk to an Active Directory and given Acegi&#8217;s flexibility you can pretty much bend this configuration any way you want to fit your needs.
  </p>
  
  <p>
    I should point out that the possibility to set up all the beans in a simple TestCase instead of having to redeploy and test the web application made trying this out much faster. It also meant that I could try each part (e.g. the FilterBasedLdapUserSearch) in isolation.
  </p>
  
  <p>
    Also, the power of Acegi is astounding. Given some (usually quite complex) configuration, it can be tweaked to perform authentication and authorization in pretty much any way imaginable. Very impressive and a great addition to Spring. Hopefully the new configuration support in Spring 2.0 will simplify the XML, I haven&#8217;t yet had the possibility to play with it.
  </p>
  
  <p>
    Ah, glad to get that of my chest. Feedback, improvements are of course welcome!
  </p>
</div>