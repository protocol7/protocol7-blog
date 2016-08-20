---
id: 1624
title: Building Despotify on Ubuntu
date: 2009-02-24T22:11:16+00:00
author: Niklas
layout: post
guid: http://protocol7.com/?p=1624
permalink: /archives/2009/02/24/building-despotify-on-ubuntu/
openid_comments:
  - 'a:8:{i:0;s:5:"86755";i:1;s:5:"93683";i:2;s:5:"93685";i:3;s:5:"93691";i:4;s:5:"93785";i:5;s:6:"101061";i:6;s:6:"101227";i:7;s:6:"101368";}'
categories:
  - Uncategorized
tags:
  - despotify
  - Linux
  - Music
  - spotify
  - ubuntu
---
<div class='microid-2ae9a1af62c39e5c0fdde0e3ad2e268656870194'>
  <p>
    Despotify is out, here&#8217;s how to build and run it on Ubuntu
  </p>
  
  <pre>
sudo apt-get install libssl-dev zlib1g-dev libvorbis-dev libpulse-dev libexpat1-dev libncurses5-dev
wget http://downloads.sourceforge.net/despotify/despotify-r761.tar.gz?use_mirror=freefr
tar xvf despotify-r761.tar.gz
cd despotify-r761/
make
./despotify &lt;your username> &lt;/your>&lt;your password>
&lt;/your></pre>
  
  <p>
    Now enjoy your text based GUI
  </p>
  
  <p>
    <img src="http://protocol7.com/wp/wp-content/uploads/2009/02/despotify.png" alt="Despotify GUI" title="Despotify GUI" width="666" height="465" class="alignnone size-full wp-image-1625" srcset="http://protocol7.com/wp/wp-content/uploads/2009/02/despotify.png 666w, http://protocol7.com/wp/wp-content/uploads/2009/02/despotify-300x209.png 300w" sizes="(max-width: 666px) 100vw, 666px" />
  </p>
</div>