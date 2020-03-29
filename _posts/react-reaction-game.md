---
title: Learn React by projects - reaction game
author: Mike Chan
layout: default
tags: [web development, bootstrap, react]
comments: true 
---

## Introduction
This post is a tutorial for making your first react app - an reaction game. Basically, this is an app that  a signal would popped out at any time and user should press the button whenever the signal is popped up. After building this app, you should be able to know some basic on what a component is.

<!--more-->

## Start a react project

To start a react project, simply type below in the console:

```
npx create-react-app reaction-game
```

After waiting a few minutes, a project structure of reaction-game is created as below:-

```
reaction-game
├── build
├── node_modules
├── public
│   ├── favicon.ico
│   ├── index.html
│   └── manifest.json
├── src
│   ├── App.css
│   ├── App.js
│   ├── App.test.js
│   ├── index.css
│   ├── index.js
│   ├── logo.svg
│   └── serviceWorker.js
├── .gitignore
├── package.json
└── README.md
```
Now, if you type ```npm start``` in console, you will see something like below.

Congradulation! You have successfully setup your React app.

## Including Bootstrap into your React App

Bootstrap is a tools that allows our website look good. To install bootstrap, in console, type ```npm i bootstrap```.

Then, goto index.js, add following line in the header:

```
import 'bootstrap/dist/css/bootstrap.css';
```

## Making Components
React's core concept is to build resusable components for front-end. Thus, learning how to create a component is a core part in React learning process. There are two types of React components. They are class Component and Functional Component. 
