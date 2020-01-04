---
title: Hacking with Pi (Part 3) - Basic Kali Linux Command
author: Mike Chan
layout: default
tags: [Kali Linux, Hacking, RaspberryPi]
---

This passage introduces some basic command to operate Kali Linux. As suggested by its name, Kali Linux one of the Linux distributions. Thus, its commands are basically the same as general Linux commands like ```ls```, ```cd``` etc. So, let's begin

<!--more-->

## Common commands of Linux in daily operation

### pwd
In Linux, it always help to know where your current location is. ```pwd``` is the one do the magic. For example, when you open your console and enter ```pwd```:

```
root@kali:~# pwd
/root
```
It shows that your location is in ```/root```. 

### ls
```ls``` stands for list. It is an common commands used in Linux. By typing ```ls``` in your console. It will list all the files in the directory at your current location. For example, if you are at ```/root```, entering ```ls``` would give you a list of directories, files in ```/root```. If your Kali with Pi is newly set up, it should show something like:

```
root@kali:~# ls
Desktop    Downloads  Pictures  Templates  Documents
Music      Public    Videos     scripts
```

If you want to list the files in other directories (e.g. ```/boot```) that is not your current location (e.g. ```/root```). Apart from moving your current location to ```/boot```, you can also enter ```ls /boot``` in console.  

```
root@kali:~# ls /boot
COPYING.linux             bcm2710-rpi-3-b.dtb  fixup4x.dat       start.elf
LICENCE.broadcom          bcm2710-rpi-cm3.dtb  fixup_cd.dat      start4.elf
armstub8-gic.bin          bcm2711-rpi-4-b.dtb  fixup_db.dat      start4cd.elf
bcm2708-rpi-b-plus.dtb    bootcode.bin         fixup_x.dat       start4db.elf
bcm2708-rpi-b.dtb         cmdline.txt          kernel.img        start4x.elf
bcm2708-rpi-cm.dtb        config.txt           kernel7.img       start_cd.elf
bcm2708-rpi-zero-w.dtb    fixup.dat            kernel7l.img      start_db.elf
bcm2708-rpi-zero.dtb      fixup4.dat           kernel8-alt.img   start_x.elf
bcm2709-rpi-2-b.dtb       fixup4cd.dat         kernel8l-alt.img
bcm2710-rpi-3-b-plus.dtb  fixup4db.dat         overlays
```

### cd
```cd``` is another common command used in Linux as well. It allows you to move your current location from directory to directoy in Linux. For example, if you are at ```/root```, and you want to enter one of the directories in its say ```Desktop```, you can type ```cd Desktop``` to enter this folder. If you want to move back to ```/root```, you can simply type ```cd ..```, then you would back up to ```/root``` directory. Also, if you want to go to ```/root```, you can alway type ```cd ~``` no matter where you are.

```
root@kali:~# cd Desktop
root@kali:~/Desktop# cd ..
root@kali:~# cd ~
root@kali:~#
```

For ```cd```, one thing you need to pay additional attention to is absolute path and relative path. Absolute path means the full path of the directory or file. It always start with /. For example, directory ```Desktop```'s absolute path is ```/root/Desktop```. It doesn't change no matter where your current location is. So, you can type ```cd /root/Desktop``` to reach this folder no matter where you are. In the example we shown previous paragraph, you hit ```cd Desktop``` in ```/root``` directory, it is relative path. It only works when you are at ```/root```.

### mkdir
```mkdir``` allows you to create a directory. For example, ```mkdir test``` in ```/root``` will create a directory ```/root/test```. 

### nano
```nano``` is a builtin text editor of Linux. Typing ```nano test.txt``` would allows you to create a file called ```test.txt``` and edit it. Upon complete of editing the file, you can hit ```Ctrl+O``` to save the file and ```Ctrl+X``` to exit the file editor.

### mv and rm
```mv``` and ```rm``` are two different commands. ```mv``` means to move a file from one directory to another. For example, you can type ```mv /root/test/test.txt /root/test.txt```. That means to move ```test.txt``` from ```/root/test``` to ```/root```. ```rm``` is to remove a file. For example, ```rm test.txt``` means remove the file ```test.txt``` from the system.


## Some commands for networking
Apart from some command for daily operation, you can also use command for checking network status etc.

### ifconfig
Typing ```ifconfig``` in your console would shows something like below:

```
eth0: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
        ether b8:27:eb:ef:d4:34  txqueuelen 1000  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

wlan0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.1.10  netmask 255.255.255.0  broadcast 192.168.1.255
        inet6 fe80::c851:b340:7b14:c5f1  prefixlen 64  scopeid 0x20<link>
        ether b8:27:eb:ba:81:61  txqueuelen 1000  (Ethernet)
        RX packets 283  bytes 20828 (20.3 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 167  bytes 38479 (37.5 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
 ```
 
 Above shows three different blocks. They are eth0, lo and wlan0. eth0 means connection using cable. It shows that the device is not connecting to any lan cable for internet service. lo stands for local machine. It shows that your local address is 127.0.0.1. wlan0 means wireless lan. In the other words, it shows your wifi connection. It shows that your device is connected to wifi with ip address of 192.168.1.19 as your ip address within the wifi network. 
 
 ### curl
 ```curl``` is a tool allow you to transfer data from and to server. For example, if you want to get the html file from google. You can simply input 
 
 ```curl www.google.com```
  
  Then, you will get the response of the html code of the www.google.com page. Apart from, 
 

 
        
