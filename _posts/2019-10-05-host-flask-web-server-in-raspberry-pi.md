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

Now, let's try if the flask app can run properly. Let's type ```FLASK_APP=helloapp.py``` to identify helloapp.py as the major flask app. Then type ```flask run``` to fireup the server. Now, type ```ifconfig``` in console to check the ip address of your device. If your pi is connected to router via wifi, you should check the one under wlan. It should shows something like this:

```
wlan0     Link encap:Ethernet  HWaddr 00:24:2c:3b:f8:79  
          inet addr:192.168.1.102  Bcast:192.168.1.255  Mask:255.255.255.0
          inet6 addr: fe80::224:2cff:fe3b:f879/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:509669 errors:0 dropped:0 overruns:0 frame:0
          TX packets:366807 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:715274922 (715.2 MB)  TX bytes:35266765 (35.2 MB)
```
In this case, your ip address is 192.168.1.102. Then, you can try to access the website using other devices connected to same router by type the ip address in browser. If it works, you can now move on to next step.

## Installation

After setting up our flask app, we can now move on to installing nginx and uwsgi for our upcoming steps. In console, type in following commands to download nginx and uwsgi.

```
sudo apt-get install nginx
sudo pip3 install uwsgi
```
If it shows error or not working, you can try ```sudo apt-get update``` and try again.

## Create Initiation File

Now, let's setup a initiation file to configure uwsgi connection in ```home/pi/helloworld```. A sample uwsgi initiation file is as per below.

```code
[uwsgi]
chdir = /home/pi/helloworld  
module = helloapp:app        

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
The above config file tells the environment to look for the flask app in ```home/pi/helloworld```. The module name is ```helloapp```. Fire up the web app with one process and two threads. uid and gid are www-data. www-data is a standard linux terms to allow www-data user to access the file as read-only and without password. It is standard for web server. The file would end up create a socket file binding port 80(defined in flask). The socket file can be found in ```/tmp/helloworld.sock```. 

After we setup all these, let's check if it works. In ```home/pi/helloworld```, type ```uwsgi --ini /home/pi/helloworld/uwsgi_config.ini```. Then, open a new shell and access to pi. Type ```ls/tmp/```. If there is a file named ```helloworld.sock``` in the folder, it works! 

## Link uwsgi with NGINX
Now, let's configure the NGINX part for reverse proxy. Upon sucessful download of NGINX, let's test if NGINX works by starting it server. In console, input the following command.

```
sudo service nginx start
```

Then, type your pi's IP address in browser of a device connected to same router, you will find a NGINX site hosting there. It is because, NGINX has a default site host in ```etc/nginx/sites-enabled```. Our job is to replace this by our website built in Flask. So, let's remove the “default” file first. 

```
sudo rm /etc/nginx/sites-enabled/default
```

Then,create a new file named as “helloworld_proxy” in “/etc/nginx/sites-available/” 

```
sudo nano /etc/nginx/sites-available/helloworld_proxy
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

The config file tells NGINX to listen on port 80 and pass all parameters to ```helloworld.sock``` we created earlier. Now, we need to link this file to ```/etc/nginx/sites-enabled```

```
sudo ln -s /etc/nginx/sites-available/sample_app_proxy /etc/nginx/sites-enabled
```
Now, restart NGINX Service 

```
sudo service nginx restart
```

Now, when you access by typing in pi's IP address again, you should see your website built with flask.

