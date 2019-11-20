---
title: How to host a Flask web server in Raspberry Pi using Nginx and uswgi
author: Mike Chan
layout: default
tags: [web development, Flask, Raspberry]
comments: true 
---

This tutorial shows a simple example in how to deploy a Flask web app in Raspberry Pi using Nginx and uwsgi.

<!-more->

#Why do we need Nginx and uwsgi?

As you may know, Flask has its own built-in server. However, this server mainly used development stage and is used for development convenience. However, 
when your project comes to production, its built-in server would be very slow to response to request.Thus,we would need a HTTP server (i.e. Nginx) and a uwsgi server
to connect the HTTP server with our flask web app. In this tutorial, we would only deploy a simple "hello world" flask web app. 

# Installation

# Nginx Initiation File

# Simple testing on Nginx File

#
