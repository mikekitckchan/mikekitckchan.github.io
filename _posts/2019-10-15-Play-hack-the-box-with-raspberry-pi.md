---
title: Play Hack The Box in Raspberry Pi
author: Mike Chan
layout: default
tags: [Kali Linux, Hacking, RaspberryPi]
comments: true 
---

This tutorial will introduce how you download Kali Linux to Raspberr Pi and connect Hack the Box with it. Happy Hacking!

<!--more-->

## Seal Kali Linux image using Mac

First, you need to insert an SD card to your Mac. Then, turn on your diskutil in Macbook to check if it is properly connected. If it is not a new SD card, right click on the hard drive of SD card and press erase, you may format the SD card to MS Dos and Master Boot Record. At the same time, find out which disk number of the SD card (e.g. disk2). 

Then, download kali linux from https://www.offensive-security.com/kali-linux-arm-images/. Choose the one under Raspberry Pi Foundation. Please pay attention that the image file download was compressed in ```.xz```. Thus, you need to uncompress as following:

```
$ sudo apt-get install xz-utils
$ xz --decompress file.xz (Replace file by actual file name)
```
The above command would uncompress and save the .img file in the same directory. Then, type ```diskutil unmountDisk diskn``` (Replace the n with the disk number of your sd card)to unmount. 

```
sudo dd bs=1m if=/[path]/[filename].img of=/dev/rdiskn conv=sync
```
Remeber to rename and path, file name and disk number of your SD card in above command. When completed, the image of Kali Linux is successfully sealed to your SD card.

## Setup in Pi
Now, you can connect your pi to a monitor. It is recommended to get a 5"-7" screen for your setup. You may need further configuration if you need to connect to some larger monitor with HDMI. Now, when the os is booted up, it would ask you for username and password. Kali Linux username is ```root``` and its password is ```toor```. When you get in, open your console and setup new password by type ```passwd root``` in console within pi. Then, install openSSH server and update the runlevels to allow SSH to start on boot.
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
