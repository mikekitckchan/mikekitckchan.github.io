---
title: How to host a Flask web server in Raspberry Pi using Nginx and uswgi
author: Mike Chan
layout: default
tags: [web development, Flask, Raspberry]
comments: true 
---

This tutorial shows a simple example in how to deploy a Flask web app in Raspberry Pi using Nginx and uwsgi.

<!--more-->

## Why do we need Nginx and uwsgi?

As you may know, Flask has its own built-in server. However, this server mainly used development stage and is used for development convenience. However, when your project comes to production, its built-in server would be very slow to response to request.Thus,we would need a HTTP server (i.e. Nginx) and a uwsgi server to connect the HTTP server with our flask web app. In this tutorial, we would only deploy a simple "hello world" flask web app. 

## Making a flask app
To begin, it always a good practice to create a virtual environment for a python project. So, let's create one for our web app at ```console /home/pi```

```console
virtualenv helloworld
```
Then, go into the virtual environment. Activate the virtual environment and install flask for the web app.

```console
cd virtualenv
source bin/activate
pip install flask
```
Then, create an helloapp.py as the major flask web app of the project. Inside app.py, we just write a siple hello world web app.

```python
from flask import Flask
app = Flask(__name__)

@app.route("/")
    def hello():
        return "Hello World!"

if __name__ == "__main__":
    app.run()
```

## Installation

After setting up our flask app, we can now move on to installing nginx and uwsgi for our upcoming steps.

```console
sudo apt-get install nginx
sudo pip3 install uwsgi
```
If it shows error or not working, you can try sudo apt-get update and try again.

## Create Initiation File

Now, let's setup a initiation file to configure uwsgi connection. A sample uwsgi initiation file is as per below.

```code
[uwsgi]
chdir = /home/pi/helloworld  #This points to the folder 
module = helloapp:app        #This tells which module is our major flask web app

master = true                #It 
processes = 1
threads = 2

uid = www-data
gid = www-data

socket = /tmp/helloworld.sock
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

