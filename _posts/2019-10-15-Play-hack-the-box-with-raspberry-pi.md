---
title: Play Hack The Box in Raspberr Pi
author: Mike Chan
layout: default
tags: [Kali Linux, Hacking, RaspberryPi]
comments: true 
---

This tutorial will introduce how you download Kali Linux to Raspberr Pi and connect Hack the Box with it. Happy Hacking!

<!--more-->

## Seal Kali Linux image using Mac

First, you need to insert an SD card to your Mac. Then, turn on your diskutil in Macbook to check if it is properly connected. 
You may format the SD card to MS Dos and Master Boot Record 

Download Kali linux to pi using Mac

1. Connect SD card to Mac
2. Format the SD card to MS Dos and Master Boot record
3. Use disk utility find out which disk it is in or type diskutil list in terminal.
4. Find out which disk the SD card is in.
5. Download kali linux from https://www.offensive-security.com/kali-linux-arm-images/
6. diskutil unmountDisk diskn (Replace the n with the disk number of your sd card)
7. sudo dd bs=1m if=/Users/mikechan/desktop/kali-linux-2019.3a-rpi3-nexmon.img.xz of=/dev/rdisk2 conv=sync

Use Etcher
1. Connect SD card to Mac
2. Format the SD card to MS Dos and Master Boot record
3. Download kali linux from https://www.offensive-security.com/kali-linux-arm-images/
4. Connect to pi and monitor
5. Setup new password: passwd root
6. Then, nstall openSSH server and update the runlevels to allow SSH to start on boot
apt-get install openssh-server
update-rc.d -f ssh remove
update-rc.d -f ssh defaults
7. The default keys represent a huge vulnerability since anyone can guess them. Let's change them immediately by running the following commands:
cd /etc/ssh/
mkdir insecure_old
mv ssh_host* insecure_old
dpkg-reconfigure openssh-server
nano /etc/ssh/sshd_config
Chang PermitRootLogin without-password -> PermitRootLogin yes
