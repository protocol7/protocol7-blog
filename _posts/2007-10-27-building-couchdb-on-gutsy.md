---
id: 1536
title: Building CouchDB on Gutsy
date: 2007-10-27T21:12:01+00:00
author: Niklas
layout: post
guid: http://protocol7.com/archives/2007/10/27/building-couchdb-on-gutsy/
permalink: /archives/2007/10/27/building-couchdb-on-gutsy/
tags:
  - couchdb
---
<div class='microid-a30b5681135897897d513158888f839c30ef2159'>
  <p>
    <img src="http://protocol7.com/wp/wp-content/uploads/2007/10/logo1.png" class="post-logo" /> Today I installed a very basic Gutsy box just to try out some stuff. The first thing was to try out the new <a href="http://couchdb.org">CouchDB</a> features, including their new build system. I used the <a href="http://blog.ciarang.com/index.php/archives/150">instructions by Ciaran Gultnieks</a> with a few small changes. Worked excellent.
  </p>
  
  <p>
    <code>&lt;br />
sudo apt-get install libicu36 libicu36-dev libreadline5-dev&lt;br />
sudo apt-get install subversion-tools xsltproc automake libtool&lt;br />
sudo apt-get install erlang&lt;br />
svn co http://couchdb.googlecode.com/svn/trunk/ couchdb&lt;br />
cd couchdb&lt;br />
./bootstrap&lt;br />
./configure --with-erlang=/usr/lib/erlang&lt;br />
make&lt;br />
sudo make install&lt;br />
</code>
  </p>
  
  <p>
    As you noticed, the differences are that I needed to install Erlang and Debian/Ubuntu sticks it in /usr/lib/erlang rather than /usr/local/lib/erlang. I also used the latest trunk, not a fixed revision. After building, you start it with:
  </p>
  
  <p>
    <code>&lt;br />
couchdb&lt;br />
</code>
  </p>
  
  <p>
    After which you can connect to CouchDB at <a href="http://localhost:8888">http://localhost:8888</a> and specifically the new amazing util client at <a href="http://localhost:8888/_utils/">http://localhost:8888/_utils/</a>. CouchDB is very slick.
  </p>
</div>