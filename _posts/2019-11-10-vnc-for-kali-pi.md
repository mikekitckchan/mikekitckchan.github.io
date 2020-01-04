---
title: Hacking with Pi (Part 2): setup VNC server 
author: Mike Chan
layout: default
tags: [Kali Linux, Hacking, RaspberryPi]
comments: true 
---

If you want to share your your Pi's screen to your mac, you can do it via VNC. It allows your electronic devices such as your Macbook, or laptop with MS windows to access your Kali Linux os in your Pi with an viewable desktop.

<!--more-->

## setup VNC for the Pi

At first, download tightvnc to your pi.

```sudo apt-get install tightvncserver```

Then, start the server by enterring the command below in console.

```vncserver :1```

The number specified after : means the TCP port number and it counts from 5900. Thus, the command above is to start its VNC server and listen at port 5901.

Now, try to check if the VNC server is working. So, in your console, type:

```netstat -tupln```

Then, your console would show something like this:

```
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name    
tcp        0      0 0.0.0.0:5901            0.0.0.0:*               LISTEN      674/Xtightvnc       
tcp        0      0 0.0.0.0:6001            0.0.0.0:*               LISTEN      674/Xtightvnc       
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      492/sshd            
tcp6       0      0 :::22                   :::*                    LISTEN      492/sshd            
udp        0      0 0.0.0.0:68              0.0.0.0:*                           577/dhclient        
udp        0      0 0.0.0.0:68              0.0.0.0:*                           373/dhclient        
```
In the first line, it shows that the tightvnc is listenning on 5901 and waiting for vnc client to connect.

Apart from just firing up your VNC server with default setting, you can also fire up with your favourite setting. Below is one of the examples:

```vncserver :1 -geometry 1280x800 -depth 16 -pixelformat rgb565```

## Setup an VNC client on Mac

There are a lot of VNC viewers to choose for Mac. The one I use in this example would be Real VNC. You can download from the link below:

https://www.realvnc.com/en/connect/download/viewer/macos/

Then, just follow the installation instruction and open the app from Mac. Then, connect to [Pi ip address]:5901. You should be able to see the screen of your Pi from your Mac.

## To start VNC server on boot

If you want to start your VNC server on boot. 

```nano /etc/init.d/vncboot```

```
#!/bin/sh
### BEGIN INIT INFO
# Provides: vncboot
# Required-Start: $remote_fs $syslog
# Required-Stop: $remote_fs $syslog
# Default-Start: 2 3 4 5
# Default-Stop: 0 1 6
# Short-Description: Start VNC Server at boot time
# Description: Start VNC Server at boot time.
### END INIT INFO

USER=root
HOME=/root

export USER HOME

case "$1" in
start)
echo "Starting VNC Server"
#Insert your favoured settings for a VNC session
/usr/bin/vncserver :1 -geometry 1280x800 -depth 16 -pixelformat rgb565
;;

stop)
echo "Stopping VNC Server"
/usr/bin/vncserver -kill :1
;;

*)
echo "Usage: /etc/init.d/vncboot {start|stop}"
exit 1
;;
esac

exit 0
```

Then, you can start VNC server by

```vncboot start``` 

and stop it by

```vncboot stop```

To enable it on boot, simply type the following:

```
chmod 755 /etc/init.d/vncboot
update-rc.d vncboot defaults
```





