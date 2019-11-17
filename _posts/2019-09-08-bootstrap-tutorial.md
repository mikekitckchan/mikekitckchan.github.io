---
title: A Beginner Guide to Bootstrap (Part 1)
author: Mike Chan
layout: default
tags: [web development, bootstrap]
comments: true 
---



<p>
Bootstrap is an opensource tool for website design using HTML, CSS and Javascript. It is very powerful for developing Responsive Web Development (RWD). This tutorial would discuss some basic skills in how to use this powerful tool in your web development. 
</p>
<!--more-->

So, to begin, how to setup? To include bootstrap in your project, you don't need to install or download anything. You can simply go to https://getbootstrap.com. And click get started.



Then, you would find a template like the one below.

```html
<!doctype html>
<html lang="en">
  <head>
    <!-- Required meta tags -->
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">

    <!-- Bootstrap CSS -->
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css" integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T" crossorigin="anonymous">
  </head>
  <body>
   

    <!-- Optional JavaScript -->
    <!-- jQuery first, then Popper.js, then Bootstrap JS -->
    <script src="https://code.jquery.com/jquery-3.3.1.slim.min.js" integrity="sha384-q8i/X+965DzO0rT7abK41JStQIAqVgRVzpbzo5smXKp4YfRvH+8abtTE1Pi6jizo" crossorigin="anonymous"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.14.7/umd/popper.min.js" integrity="sha384-UO2eT0CpHqdSJQ6hJty5KVphtPhzWj9WO1clHTMGa3JDZwrnQq4sF86dIHNDz0W1" crossorigin="anonymous"></script>
    <script src="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/js/bootstrap.min.js" integrity="sha384-JjSmVgyd0p3pXB1rRibZUAYoIIy6OrQ6VrjIEaFf/nJGzIxFDsf4x0xIM+B07jRM" crossorigin="anonymous"></script>
  </body>
</html>
```

That's it! Setting up bootstrap is as simple as that. Now, you are ready to make your website using Bootstrap.

## A Basic Grid System of Bootstrap


Before start our coding, lets understand what is a grid system in Bootstrap. In Bootstrap, you can control the size of each div by grid. Bootstrap grid system divide a screen into 12 columns. For example, if you tell Bootstrap that your div class would occupies 12 columns, it means that your div class would occupies 100% of the screen width. If your div class occupies 6 columns, it would be half of the screen. Also, you can design your div class to occupies different screen width for different devies. For example, you can tell Bootstrap that your div class would occupies 12 columns for large devices like desktop but just 6 columns for mid-sized devies like laptop. Then you can simply define it by <div class = "col-lg-12 col-md-6">.  A list of definition syntax is as shown in table below:

|                                | For small devices         | For mid-sized devices     | For large devices         |
| ------------------------------ | ------------------------- | ------------------------- | ------------------------- |
| Occupying 25% of screen width  | <div class = "col-sm-3">  | <div class = "col-md-3">  | <div class = "col-lg-3">  |
| Occupying 50% of screen width  | <div class = "col-sm-6">  | <div class = "col-md-6">  | <div class = "col-lg-6">  |
| Occupying 75% of screen width  | <div class = "col-sm-9">  | <div class = "col-md-9">  | <div class = "col-lg-9">  |
| Occupying 100% of screen width | <div class = "col-sm-12"> | <div class = "col-md-12"> | <div class = "col-lg-12"> |

Let's put it in practice, if you would like to make your paragraph occupies half of the screen's width, you can simply use the following code inside <body>:

```html
<body>
	<div class="col-md-6 col-lg-6 col-sm-6">
		<p>
      This only occupies half of the screen's width! 
      This only occupies half of the screen's width! 
      This only occupies half of the screen's width! 
      This only occupies half of the screen's width! 
      This only occupies half of the screen's width! 
      This only occupies half of the screen's width! 
      This only occupies half of the screen's width! 
      This only occupies half of the screen's width! 
      This only occupies half of the screen's width! 				
      This only occupies half of the screen's width! 
      This only occupies half of the screen's width! 
      This only occupies half of the screen's width! 
      This only occupies half of the screen's width! 
      This only occupies half of the screen's width! 
    </p>
	</div>
</body>
```

It will shows something like below on your screen:

<span class="image"><img src="{{ 'assets/images/bootstraptutorial1.png' | relative_url }}" alt="" /></span>

Using this grid system, you can design some text alignment like below:-

```html
<div class = "row">
	<div class="col-md-3">
		<p>Name: </p>
	</div>
  <div class="col-md-3">
		<p>Peter </p>
	</div>
 </div>
<div class = "row">
	<div class="col-md-3">
		<p>Age: </p>
	</div>
  <div class="col-md-3">
		<p>17</p>
	</div>
 </div>
```

It will shows something like this:

<span class="image"><img src="{{ 'assets/images/bootstraptutorial2.png' | relative_url }}" alt="" /></span>

So, I made two rows and two columns, each column occupies around 1/4 of the screen's width.

However, the example above doesn't look nice as everything is aligned top and left. In Bootstrap, you can put everything into a container for easy management. Using the previous example, you can amend slightly like below:

```html
<body>
    <div class = "container col-md-6">
        <div class = "row">
            <div class="col-md-6">
                <p>Name: </p>
            </div>
            <div class="col-md-6">
                <p>Peter </p>
            </div>
        </div>
        <div class = "row">
            <div class="col-md-6">
                <p>Age: </p>
            </div>
            <div class="col-md-6">
                <p>17</p>
            </div>
        </div>
  </div>
    <style>
    .container {
                position: absolute;
                left: 30%;
                top: 25%;
            }
    </style>
  </body>
```

In the example above, we put everything in a container. Then we can use css to place the container 30% from the left and 25% from the top. Now, it look much better than before:

<span class="image"><img src="{{ 'assets/images/bootstraptutorial3.png' | relative_url }}" alt="" /></span>

## Adding Bootstrap default Component

In Bootstrap, there are many built-in components like navbar and buttons etc. You can find these all from www.getbootstrap.com. For example, if you go to https://getbootstrap.com/docs/4.3/components/buttons/, you can find different kind of buttons and from the scroll down list on the left hand side, you can also find other components such as navbar and stuff.

In the next sections, we would started applying the basic concepts above in real life examples.
