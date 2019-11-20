---
title: A Beginner Guide to Bootstrap (Part 2) - Login Page
author: Mike Chan
layout: default
tags: [web development, bootstrap]
category: bootstrap
---




This would be our first section in introducing how to use bootstrap in real life example. At first, putting the neccessary CDN 
link of bootstrap within ```<head> ```. If you are not familar with how to include CDN of Bootstrap into your project, please refer to the first session of this series. Then, we can start making our login page.
 
<!--more-->

## Container
As per the first section, we can put everything into a container for easy management. We can start off our first version of login page as below:

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
    <div id="login" class="container">
        

        <form>
            <div class="form-group">
                
                <input type="email" class="form-control" id="InputEmail" placeholder="Enter email">
                <input type="password" class="form-control" id="InputPassword" placeholder="Enter password">
                <button type="button" class="btn btn-light">Submit</button>
                
            </div>
        </form>
    </div>
        

  
</body>
```
So, in our first version, we put a form-group into a container. A form-group is a kind of components in Bootstrap. For details, you can check out more from getbootstrap.com. The codes above would shows you something like below:

<img src="{{ 'assets/images/posts/bootstrap-tutorial-2/bootstrap21.png' | relative_url }}" alt="" />

But as you can see, the login page looks very ugly as all the input field are aligned to the top of the screen. Also, the email and password fields are too close to each other. To solve this problem, we can put the two input a form-row div class. Then, in the div class, set its top padding to 4px to separate these two rows. To do this, you can simply put pt-4 inside the div class. pt stands for padding top. So, the codes of form-group would be look something like below:

```html
<form>
  <div class="form-group">
    <div class = "form-row pt-4">
      <input type="email" class="form-control" id="InputEmail" placeholder="Enter email">
    </div>
    <div class = "form-row pt-4">
      <input type="password" class="form-control" id="InputPassword" placeholder="Enter password">
    </div>
    <div class = "form-row pt-4">
      <button type="button" class="btn btn-light">Submit</button>
     </div>
  </div>
</form>
`
To move the whole things down to around middle of the screen, you can simply add some ccs code to move the whole container down. You can do something like this:

`
<style>
    .container{
        margin-top: 25%;
    }
</style>
```
This is to tell the browser to place container to place a margin at top to around 25% of the screen. So, combining the two codes above, the result would look something like this:

<img src="{{ 'assets/images/posts/bootstrap-tutorial-2/bootstrap22.png' | relative_url }}" alt="" />

So, now. Still not quite yet. I think we should add a header to the login box. Also, I think the login box to too wide. So, I would put col-md-6 into container div class to set the whole container's width to be half of the screen. Then, I would add border line to the container. A complete code of the whole things can look something like below:

```html
<body>

    <div id="login" class = "container col-md-6">
        <form>
            <h1> Welcome to my Login Page</h1>
            <div class="form-group">
                <div class = "form-row pt-4">
                    <input type="email" class="form-control" id="InputEmail" placeholder="Enter email">
                </div>
                <div class = "form-row pt-4">
                    <input type="password" class="form-control" id="InputPassword" placeholder="Enter password">
                </div>
                <div class = "form-row pt-4">
                    <button type="button" class="btn btn-light">Submit</button>
                </div>
            </div>
        </form>
    </div>

    <style>
    .container{
        margin-top:25%;
        border-radius: 2px;
        border: 2px solid #B62B96;
    }
    </style> 
</body>
```
And the result would be look like this:

<img src="{{ 'assets/images/posts/bootstrap-tutorial-2/bootstrap23.png' | relative_url }}" alt="" />

Well, that looks much better. I will take this. Now, you can make one up for your own project.
