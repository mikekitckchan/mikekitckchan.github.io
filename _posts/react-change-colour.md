---
title: Learn React by projects part 1- colour changer
author: Mike Chan
layout: default
tags: [web development, bootstrap, react]
comments: true 
---

## Introduction
This post is a tutorial for making your first react app to change colour of a button. Basically, this is an app that the button would be changed everytime you click it. After building this app, you should be able to know some basic on what a React App is built, how to integrate with Bootstrap and what a component is.

<!--more-->

## Start a react project

To start a react project, simply type below in the console:

```
npx create-react-app colour-changer
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

Bootstrap is a tools that allows our website look good. To install bootstrap, in console, type ```npm install react-bootstrap bootstrap```.

Then, goto index.js, add following line in the header:

```
import 'bootstrap/dist/css/bootstrap.css';
```

## Making Components
React's core concept is to build resusable components for front-end. Thus, learning how to create a component is a core part in React learning process. To start with, you may add a folder named ```components``` under ```src``` folder. It is a good practice to put all your components files under this folder. In this example, let's create a component called ```colorchanger.js```. In ```colorchanger.js```,  

```javascript
import React, {Component} from 'react';

class colorChanger extends Component{
	state={

	}

	render(){
		
	};

} 

export default colorChanger;
```


