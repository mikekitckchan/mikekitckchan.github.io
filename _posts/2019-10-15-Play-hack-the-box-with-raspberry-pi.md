---
title: Set up Kali Linux on Raspberry Pi
author: Mike Chan
layout: default
tags: [Kali Linux, Hacking, RaspberryPi]
comments: true 
---

Kali Linux is a kind of Linux distributions specialized in penetration testing. It has several hundreds penetration test built-in tools such as Nmap, Sparta etc. This tutorial introduces a step by step guide on how to setup Kali Linux to your Raspberry Pi using Mac.

<!--more-->

## Seal Kali Linux image using Mac

First, insert an SD card to your Mac. Then, turn on your diskutil in Macbook to check if it is properly connected. If it is not a new SD card, right click on the hard drive of SD card and press erase, format the SD card to MS Dos and Master Boot Record. At the same time, find out which disk number of the SD card (e.g. disk2). 

Then, download kali linux from https://www.offensive-security.com/kali-linux-arm-images/. Choose the one under Raspberry Pi Foundation. Please pay attention that the image file download was compressed in ```.xz```. Thus, you need to uncompress as after you dowload:

```
$ gunzip filename.xz
```
The above command would uncompress and save the .img file in the same directory. Then, type ```diskutil unmountDisk disk2``` (Replace the disk2 by the disk number of your sd card)to unmount. Then, start write the Kali Linux into your SD card.

```
sudo dd bs=1m if=/[path]/[filename].img of=/dev/rdisk2 conv=sync
```
Remeber to rename and path, file name and disk number of your SD card in above command. When completed, the image of Kali Linux is successfully sealed to your SD card.

## Configuration in Pi
Now, you can connect your pi to a monitor. Now, when the os is booted up, it would ask you for username and password. Kali Linux default username is ```root``` and its default password is ```toor```. When you get in, open your console and setup new password by inputting ```passwd root``` in console. Upon successful changing of password, install openSSH server and update the runlevels to allow SSH to start on boot.
```
apt-get install openssh-server
update-rc.d -f ssh remove
update-rc.d -f ssh defaults
```

The default keys represent a huge vulnerability since anyone can guess them. Let's change them immediately by running the following commands:
```
cd /etc/ssh/
mkdir insecure_old
mv ssh_host* insecure_old
dpkg-reconfigure openssh-server
nano /etc/ssh/sshd_config
```
Find ```PermitRootLogin without-password``` and make sure  ```PermitRootLogin yes``` exists.

So, configuration of your Pi is basically completed. You can try to use its inbuilt tools to port scan other devices within your netowrk or play Hack the Box to hunt down some machines. Happy hacking!
