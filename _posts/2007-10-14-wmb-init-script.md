---
id: 1530
title: WMB init script
date: 2007-10-14T21:23:24+00:00
author: Niklas
layout: post
guid: http://protocol7.com/archives/2007/10/14/wmb-init-script/
permalink: /archives/2007/10/14/wmb-init-script/
tags:
  - Applications
  - Messaging/JMS
  - MQ
---
<div class='microid-6a130dc2dd1baf430da0175b22433cb7db835c46'>
  <p>
    For a client, I recently had to install a <a href="http://www.ibm.com/software/integration/wbimessagebroker/">WebSphere Message Broker</a> on <a href="http://www.novell.com/products/server/">Suse Linux</a>. This also means getting it to start at boot time. Now, as far as I&#8217;ve been able to locate, WMB does not come with a init script. For WebSphere MQ, IBM recently added a <a href="http://www-1.ibm.com/support/docview.wss?rs=171&uid=swg24016554&loc=en_US&cs=utf-8&lang=en">service pac, MSL1</a>, that does exactly this, but so far no luck for WMB. SLES uses <a href="http://refspecs.linux-foundation.org/LSB_3.1.0/LSB-Core-generic/LSB-Core-generic/iniscrptact.html">LSB compliant init scripts</a>, and has a command called <a href="http://susefaq.sourceforge.net/faq/services.html">insserv</a> which automatically sets up the soft links to make all components start it the right order based on the dependencies you define as metadata in your script. So, with no further ado, here&#8217;s my current stab at the script:
  </p>
  
  <pre>
#!/bin/sh
### BEGIN INIT INFO
# Provides:          wmb
# Required-Start:    $syslog $network $remote_fs ibm.com-WebSphere_MQ 
# Should-Start:      db2
# Required-Stop:     $syslog $network
# Should-Stop: 
# Default-Start:     3 5
# Default-Stop:      0 1 2 6
# Short-Description: WebSphere Message Broker
# Description:       Starts WebSphere Message Broker
### END INIT INFO

# Source /etc/rc.status:
. /etc/rc.status

# Reset status of this service
rc_reset

case "$1" in
    start)
    	echo -n "Starting WMB "
    	su - mqm -c 'mqsistart BRK1D;mqsistart CFGMGRD'
    
    	# Remember status and be verbose
    	rc_status -v
	  ;;
    stop)
    	echo -n "Shutting down WMB "
    	su - mqm -c 'mqsistop BRK1D;mqsistop CFGMGRD'
    
    	# Remember status and be verbose
    	rc_status -v
	  ;;
    try-restart|condrestart)
	    ## Do a restart only if the service was active before.
	    $0 status
    	if test $? = 0; then
    		$0 restart
    	else
    		rc_reset	# Not running is not a failure.
    	fi
    	# Remember status and be quiet
    	rc_status
	  ;;
    restart)
    	## Stop the service and regardless of whether it was
    	## running or not, start it again.
    	$0 stop
    	$0 start

    	# Remember status and be quiet
    	rc_status
	  ;;
    force-reload)
    	$0 try-restart
    	rc_status
	  ;;
    reload)
	    rc_failed 3
	    rc_status -v
	  ;;
    status)
	   echo -n "Checking for service WMB "
	   /sbin/checkproc /opt/ibm/mqsi/6.0/bin/bipservice
	   rc_status -v
	  ;;
    *)
	    echo "Usage: $0 {start|stop|status|try-restart|restart|force-reload|reload}"
	    exit 1
	  ;;
esac
rc_exit
</pre>
  
  <p>
    Note that the script will start WMB as the mqm user. If this is not what you want, you will have to make your changes at the su commands.
  </p>
  
  <p>
    To use, create a file called /etc/init.d/wmb and paste the above content into. Make sure it&#8217;s runnable with:
  </p>
  
  <pre>
chmod +x /etc/init.d/wmb
</pre>
  
  <p>
    The run:
  </p>
  
  <pre>
insserv wmb 
</pre>
  
  <p>
    And it should set everything nicely for you.
  </p>
  
  <p>
    Note that this script is dependent on the WebSphere MQ init script, as provided in the support pac mentioned above. It will also start DB2 beforehand, if available. In my case, we are using DB2, I&#8217;m just not happy with the current script I got so I will hold off publishing it until I&#8217;m done.
  </p>
  
  <p>
    I will be happy to get feedback in the comments on my attempt and will update the code above with any changes.
  </p>
  
  <p>
    Technorati Tags: <a class="performancingtags" href="http://technorati.com/tag/wmb" rel="tag">wmb</a>, <a class="performancingtags" href="http://technorati.com/tag/linux" rel="tag">linux</a>, <a class="performancingtags" href="http://technorati.com/tag/ibm" rel="tag">ibm</a>, <a class="performancingtags" href="http://technorati.com/tag/suse" rel="tag">suse</a>, <a class="performancingtags" href="http://technorati.com/tag/sles" rel="tag">sles</a>, <a class="performancingtags" href="http://technorati.com/tag/lsb" rel="tag">lsb</a>, <a class="performancingtags" href="http://technorati.com/tag/wmq" rel="tag">wmq</a>, <a class="performancingtags" href="http://technorati.com/tag/websphere" rel="tag">websphere</a>
  </p>
</div>