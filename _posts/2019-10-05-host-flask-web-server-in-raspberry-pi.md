---
title: How to host a Flask web server in Raspberry Pi using Nginx and uswgi
author: Mike Chan
layout: default
tags: [web development, Flask, Raspberry]
comments: true 
---

This tutorial shows a simple example in how to deploy a Flask web app in Raspberry Pi using Nginx and uwsgi.

<!-more-->

# Why do we need Nginx and uwsgi?

As you may know, Flask has its own built-in server. However, this server mainly used development stage and is used for development convenience. However, when your project comes to production, its built-in server would be very slow to response to request.Thus,we would need a HTTP server (i.e. Nginx) and a uwsgi server to connect the HTTP server with our flask web app. In this tutorial, we would only deploy a simple "hello world" flask web app. 

# To Begin
To begin, let's create a virtual environment for our web app.

```console
root$ virtualenv helloworld
```



# Installation

```console
sudo apt-get install nginx
```
If not working, try sudo apt-get update and try again

```console
sudo pip3 install uwsgi
```


# Nginx Initiation File
Create a file called uwsgi_config.ini in your working folder.
```code
[uwsgi]
chdir = /home/pi/[your working folder]
module = helloworld:app

master = true
processes = 1
threads = 2

uid = www-data
gid = www-data

socket = /tmp/helloworld.sock
chmod-socket = 664
vacuum = true

die-on-term = true
```

# Simple testing on Nginx File
In your working folder, 
```console
uwsgi --ini /home/pi/[ ]/uwsgi_config.ini
```
Open a new shell and access to pi. Type “ls/tmp/“. There should be a file named helloworld.sock.

# Link uwsgi with NGINX
First, remove “default” file from “/etc/nginx/sites-enabled/” 

```console
sudo rm /etc/nginx/sites-enabled/default
```

Then,create a new file named as “helloworld_proxy” in “/etc/nginx/sites-available/” 

```console
sudo vi /etc/nginx/sites-available/helloworld_proxy
```
Add following configuration in “helloworld_proxy” file 

```code
server {
 listen 80;
 server_name localhost;

 location / { try_files $uri @app; }
 location @app {
 include uwsgi_params;
 uwsgi_pass unix:/tmp/helloworld.sock;
 }
}
```

Then, ink “/etc/nginx/sites-available/helloworld_proxy” file to “/etc/nginx/sites-enabled” directory:

```console
sudo ln -s /etc/nginx/sites-available/sample_app_proxy /etc/nginx/sites-enabled
```
Then, restart NGINX Service –
```console
sudo service nginx restart
```
With this your Raspberry Pi is ready with a sample Python Flask Web Application. You can type Raspberry Pi’s IP Address in your web browser to access the HTML Page.

