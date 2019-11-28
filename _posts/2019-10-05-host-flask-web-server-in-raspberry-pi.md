---
title: How to host a Flask web server in Raspberry Pi using Nginx and uswgi
author: Mike Chan
layout: default
tags: [web development, Flask, RaspberryPi]
comments: true 
---

This tutorial shows a simple example in how to deploy a Flask web app in Raspberry Pi using Nginx and uwsgi.

<!--more-->

## Why do we need Nginx and uwsgi?

As you may know, Flask has its own built-in server. However, this server mainly used in development stage and is used for development convenience. When your project comes to production, its built-in server would be very slow to response to request and has several security issues.Thus,we would need an HTTP server (i.e. Nginx) and a uwsgi server to connect the HTTP server with our flask web app. In this tutorial, we would show you how to deploy a simple "hello world" flask web app in Raspberry Pi using the above said tools. 

## Making a flask app
To begin, it always a good practice to create a virtual environment for a python project. So, let's create one for our web app . Input the following commaned to create a virtual environment helloworld in any directories you want to work at. In this example, we would create the virtual environment at ```/home/pi```.

```
python3 -m virtualenv helloworld
```

The abovesaid command is exactly the same as ```virtualenv helloworld```. But if you have both python2 and python3 in same os environment, the one mentioned beforehand would force the virtual environment using python3.

Then, go into the virtual environment by typine ```cd helloworld```. Activate the virtual environment by ```source bin/activate```. You should able to see something like ```(helloworld)~/helloworld$```in your console. Then, install flask using pip: ```pip install flask```. Now, let's create an helloapp.py as the major flask web app of the project. Inside helloapp.py, we just write a simple hello world web app as follow.

```python
#helloapp.py
from flask import Flask
app = Flask(__name__)

@app.route("/")
    def hello():
        return "Hello World!"

if __name__ == "__main__":
    app.run(host='0.0.0.0', port=80)
```

Now, let's try if the flask app can run properly. Let's type ```FLASK_APP=helloapp.py``` to identify helloapp.py as the major flask app. Then type ```flask run``` to fireup the server. Now, type ```ifconfig``` in console to check the ip address of your device. If your pi is connected to router via wifi, you should check the one under eth0. It should shows something like this:

```
eth0: flags=8863<UP,BROADCAST,SMART,RUNNING,SIMPLEX,MULTICAST> mtu 1500
	ether 8c:85:90:78:8c:9e 
	inet6 fe80::1c34:598f:712f:482d%en0 prefixlen 64 secured scopeid 0x6 
	inet 192.168.43.149 netmask 0xffffff00 broadcast 192.168.43.255
	nd6 options=201<PERFORMNUD,DAD>
	media: autoselect
	status: active
```
In this case, your ip address is 192.168.43.255. Then, you can try to access the website using other devices connected to same router by type the ip address in browser. If it works, you can now move on to next step.

## Installation

After setting up our flask app, we can now move on to installing nginx and uwsgi for our upcoming steps. In console, type in following commands to download nginx and uwsgi.

```
sudo apt-get install nginx
sudo pip3 install uwsgi
```
If it shows error or not working, you can try ```sudo apt-get update``` and try again.

## Create Initiation File

Now, let's setup a initiation file to configure uwsgi connection. A sample uwsgi initiation file is as per below.

```code
[uwsgi]
chdir = /home/pi/helloworld  #This points to the folder of where your app is.
module = helloapp:app        #This tells which module is our major flask web app

master = true                #It 
processes = 1                #It tells how many proecesses our web app need.
threads = 2                  #It tells how many threads our web app need.

uid = www-data               #these two lines tell the webapp can be access by www-data. 
gid = www-data

socket = /tmp/helloworld.sock #The file would create a socket file and 
chmod-socket = 664
vacuum = true

die-on-term = true
```

## Simple testing on Nginx File
In your working folder, 
```console
uwsgi --ini /home/pi/[ ]/uwsgi_config.ini
```
Open a new shell and access to pi. Type “ls/tmp/“. There should be a file named helloworld.sock.

## Link uwsgi with NGINX
First, input the following command in console.

```console
sudo service nginx start
```

Then, when you will find that a site i
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

Then, link “/etc/nginx/sites-available/helloworld_proxy” file to “/etc/nginx/sites-enabled” directory:

```console
sudo ln -s /etc/nginx/sites-available/sample_app_proxy /etc/nginx/sites-enabled
```
Then, restart NGINX Service –
```console
sudo service nginx restart
```
With this your Raspberry Pi is ready with a sample Python Flask Web Application. You can type Raspberry Pi’s IP Address in your web browser to access the HTML Page.

