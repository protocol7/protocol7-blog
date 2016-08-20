---
id: 1302
title: MD5 support in FtpServer
date: 2006-09-04T22:08:21+00:00
author: Niklas
layout: post
guid: http://protocol7.com/archives/2006/09/04/md5-support-in-ftpserver/
permalink: /archives/2006/09/04/md5-support-in-ftpserver/
tags:
  - Apache
  - FtpServer
cocomment_trackall:
  - 
  - 
openid_comments:
  - 'a:1:{i:0;s:5:"70620";}'
---
<div class='microid-b397b0521dfc9b64d791faa96e15b77cdb4a0f55'>
  <p>
    This weekend I checked in support for the <a href="http://www.indyproject.org/Sockets/Blogs/JPeterMugaas/draft-twine-ftpmd5-00.txt">draft-twine-ftpmd5-00</a> proposal for MD5 support in <a href="http://incubator.apache.org/ftpserver/">Apache Incubator FtpServer</a>. In short, the draft adds two new FTP commands, MD5 and MMD5. Both adds the possibility of requesting the MD5 for one (MD5 command) or multiple (MMD5 command) files. This is an important piece of functionality if you want to do automated transfers over FTP. Using the commands, a client can upload a file and then request the MD5 hash and compare it to the hash of the local file. Similary, it can request the hash of a file to be downloaded to ensure that the file is downloaded without any corruption. All in all a very useful addition to FTP. To bad the draft never seemed to have <a href="https://datatracker.ietf.org/public/idindex.cgi?command=id_detail&id=8808">gotten anywhere in the standards process</a>.
  </p>
</div>