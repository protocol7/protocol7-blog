---
id: 1542
title: Easier certificates for MQ
date: 2007-11-28T22:57:39+00:00
author: Niklas
layout: post
guid: http://protocol7.com/archives/2007/11/28/easier-certificates-for-mq/
permalink: /archives/2007/11/28/easier-certificates-for-mq/
tags:
  - MQ
  - Security
openid_comments:
  - 'a:3:{i:0;s:5:"97516";i:1;s:5:"97533";i:2;s:5:"97553";}'
categories:
  - Uncategorized
---
<div class='microid-cafa1dc2be8784a9f0058752f560181f1fff9c34'>
  <p>
    <strong>Update:</strong> I&#8217;ve posted a <a href="http://protocol7.com/archives/2008/06/29/basic-constraints-on-websphere-mq-ca-certificate/">follow up</a> to this post with an important addition to the script to create your CA certificate.
  </p>
  
  <hr />
  
  <p>
    The last couple of days I&#8217;ve been hard at work with setting up SSL for WebSphere MQ for a customer. A major part of that is creating certificates. WMQ uses the IBM security toolkit, GSKit. My previous experience with GSKit is not the best, I&#8217;ve found that it works inconsistently between versions and platforms and contains frequent bugs. Working with this time, the inconsistencies seems to still be there, but at least many of the bugs are now gone. One of the problems is that some GSKits doesn&#8217;t work with keys/certificates created with the Java keytool which has previously been my weapon of choice (with the <a href="http://www.lazgosoftware.com/kse/">Keystore Explorer GUI</a>).
  </p>
  
  <p>
    Finally giving up on keytool, I retreated to using the GSKit command line tool, gsk7cmd. Working with gsk7cmd is not the most pleasant experience (almost as bad as OpenSSL). Therefore, I&#8217;ve created a set of Linux shell scripts targeted for a streamlined flow for creating certs for WMQ. <a href="http://wmq-util.googlecode.com/svn/ssl-scripts/">They are made available</a> under the <a href="http://www.apache.org/licenses/LICENSE-2.0.html">ASL 2 license</a>. This is how they work.
  </p>
  
  <p>
    Create a directory on some server where you like to create your keys. Copy the scripts to your directory. Edit the scripts to update some generic configuration, currently the DN used and the expiration time for the certificates.
  </p>
  
  <p>
    Now start out by running create-ca.sh:
  </p>
  
  <p>
    ./create-ca.sh mySecretPassword
  </p>
  
  <p>
    Make sure you choose a strong password. The command will create a CMS key store containing your CA root certificate. Save it somewhere safe.
  </p>
  
  <p>
    Then, for each queue manager (or client), run:
  </p>
  
  <p>
    ./create-key.sh MyQueueManager mySecretPassword<br />or<br />./create-key.sh MyClientApplication mySecretPassword
  </p>
  
  <p>
    This will create a directory containing a key created for your queue manager. Its certificate will be signed by the CA root key previously created.
  </p>
  
  <p>
    If, for some reason you can not create the keys this way, try creating them on the target platform. For example, I failed to get any externally created keys working on iSeries, instead I had to use the DCM tool on the iSeries box. In this case, create the key and export a certificate request (I&#8217;ll write down the details for doing this on iSeries if anyone is interested). Save the certificate request in your keys directory created at the begining of this howto. Name it <queue manager name in lower case>.p10. Run:
  </p>
  
  <p>
    ./sign-key.sh MyQueueManager mySecretPassword
  </p>
  
  <p>
    It will create a certificate response in the file called <queue manager name in lower case>.p7r. Import this together with ca_cert.crt on your target platform.
  </p>
  
  <p>
    If your client happens to be a Java client, you need the key store in JKS format. To convert it, run the following command:
  </p>
  
  <p>
    ./convert-to-java.sh MyQueueManager mySecretPassword
  </p>
  
  <p>
    Note that the signing steps does make a huge assumption. A CA must use a unique serial number for each certificate it signs. I didn&#8217;t want the overhead of keeping track of this. Instead I use a random number for the serial number. This means that if you sign lots of certs with your CA, you might very well get collisions. If you got that many certs, you probably need a better tool :-)
  </p>
  
  <p>
    These scripts uses some ideas from <a href="http://hursleyonwmq.wordpress.com/2007/02/05/an-introduction-to-ssl-configuration/">the scripts published by Dale Lane</a>. Thanks! If you want to port these scripts to some other platform, I will happily accept them into SVN. Same goes for bugs and improvements of course.
  </p>
  
  <p>
    Technorati Tags: <a class="performancingtags" href="http://technorati.com/tag/wmq" rel="tag">wmq</a>, <a class="performancingtags" href="http://technorati.com/tag/mq" rel="tag">mq</a>, <a class="performancingtags" href="http://technorati.com/tag/security" rel="tag">security</a>, <a class="performancingtags" href="http://technorati.com/tag/ssl" rel="tag">ssl</a>, <a class="performancingtags" href="http://technorati.com/tag/gskit" rel="tag">gskit</a>
  </p>
</div>