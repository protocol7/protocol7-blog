---
id: 1522
title: WebSphere MQ security
date: 2007-08-31T12:39:57+00:00
author: Niklas
layout: post
guid: http://protocol7.com/archives/2007/08/31/websphere-mq-security/
permalink: /archives/2007/08/31/websphere-mq-security/
tags:
  - MQ
  - Security
---
<div class='microid-7335ec749c1f18f59a3beeaca059e670767e26c3'>
  <p>
    With all the recent fuzz on WebSphere MQ security I thought that I should try to collect the current thinking on the best way of securing your WMQ environment.
  </p>
  
  <p>
    <p>
      Lately, <a href="http://permalink.gmane.org/gmane.network.mq.devel/5689">T-Rob</a> and <a href="http://www.defcon.org/html/defcon-15/dc-15-speakers.html#Ruks">Martyn Ruks</a> has held two separate presentations on WMQ security and the following posts will reflect a lot of what they presented. This combined with my experiences from securing WMQ environments make up most of the content. I hope to collect feedback from the community to improve over time.
    </p>
    
    <p>
      Please note that these posts are my current understanding and should not be regarded as the final answer. I will continue to update these posts as I learn more on the topic. Any feedback is crucial so feel free to comment on any of these posts or send me an email directly. My experience is on the distributed platforms, so you&#8217;ll find very limited specifics on how to secure your z/OS environment, hopefully the community can help fill these gaps.
    </p>
    
    <p>
      Most of the topics listed below are placeholders for future posts I intend to write, and this list will most likely be heavily modified before I&#8217;m done.
    </p>
    
    <h3>
      How to create a secure WMQ environment
    </h3>
    
    <p>
      <ul>
        <li>
          Why secure?
        </li>
        <p>
          <li>
            Keep up to date
          </li>
          <p>
            <li>
              Policy
            </li>
            <p>
              <li>
                Secure by default
              </li>
              <p>
                <li>
                  Securing channels
                </li>
                <p>
                  <li>
                    Securing queues
                  </li>
                  <p>
                    <li>
                      Publish/subscribe
                    </li>
                    <p>
                      <li>
                        Triggers and services
                      </li>
                      <p>
                        <li>
                          Securing applications
                        </li>
                        <p>
                          </ul> 
                          
                          <h3>
                            Breaking in to WMQ
                          </h3>
                          
                          <p>
                            <ul>
                              <li>
                                <a href="http://protocol7.com/archives/2007/08/17/websphere-mq-message-spoofing-using-the-dead-letter-queue/">Spoofing messages using the dead letter queue</a>
                              </li>
                              <p>
                                <li>
                                  <a href="http://protocol7.com/archives/2007/08/31/websphere-mq-message-spoofing-using-confirm-on-arrival-reports/">Spoofing messages using confirm-on-arrival reports</a>
                                </li>
                                <p>
                                  </ul> 
                                  
                                  <p>
                                    Technorati Tags: <a class="performancingtags" href="http://technorati.com/tag/wmq" rel="tag">wmq</a>, <a class="performancingtags" href="http://technorati.com/tag/websphere" rel="tag">websphere</a>, <a class="performancingtags" href="http://technorati.com/tag/mq" rel="tag">mq</a>, <a class="performancingtags" href="http://technorati.com/tag/security" rel="tag">security</a>, <a class="performancingtags" href="http://technorati.com/tag/ibm" rel="tag">ibm</a>
                                  </p></div>