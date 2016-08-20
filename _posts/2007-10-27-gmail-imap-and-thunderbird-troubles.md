---
id: 1538
title: GMail IMAP and Thunderbird troubles
date: 2007-10-27T22:55:50+00:00
author: Niklas
layout: post
guid: http://protocol7.com/archives/2007/10/27/gmail-imap-and-thunderbird-troubles/
permalink: /archives/2007/10/27/gmail-imap-and-thunderbird-troubles/
tags:
  - GMail
openid_comments:
  - 'a:4:{i:0;s:5:"49997";i:1;s:5:"49998";i:2;s:5:"49999";i:3;s:5:"50000";}'
---
<div class='microid-97199b5ca8bc3f34c1123f0335ba9f89a8977757'>
  <p>
    I&#8217;m trying out the new, much hyped <a href="http://lifehacker.com/software/geek-to-live/turn-thunderbird-into-the-ultimate-gmail-imap-client-314574.php">GMail IMAP support</a>. I added the account to Thunderbird but pretty soon ran into troubles. It seems like Thunderbird has serious issues with folders containing large number of messages. My inbox currently has 65065 messages, which doesn&#8217;t seem that much. The problem manifest itself by Thunderbird being excessively slow doing anything to any mail in the inbox, some actions (like junking) not working at all. I&#8217;ve also seen Thunderbird using more than 1 Gb of RAM before I had to kill it. If I choose a folder with less messages, like one of the folders based on a GMail label, everything works as expected.
  </p>
  
  <p>
    The mouse marker is pretty much pegged in hour-glass mode, still it doesn&#8217;t seem to use that much CPU.
  </p>
  
  <p>
    I&#8217;ve noticed a similar problem before with a POP based folder that stopped working properly as it grew too large. I&#8217;ve googled and searched the <a href="https://bugzilla.mozilla.org/">Thunderbird Bugzilla</a> without finding anything obvious. Anyone got any suggestion before I add a confused bug report?
  </p>
</div>