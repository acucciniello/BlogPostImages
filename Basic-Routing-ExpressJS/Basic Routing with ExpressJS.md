# Basic Routing with ExpressJS

## Introduction

Want an easy way to have a few routes in your Node.js web application? If you answered yes, you should undestand how to do exactly that by the end of this post.  But first, what is routing? In simple terms, it is how an application is told to respond to client on a specific endpoint.  An endpoint is basically a path or URI and one of the HTTP request methods (GET, POST, etc). 

Express.js is a Node.js framework that allows you to help organize your web application on the server side.  IT is one of the most popular node packages and many of the other popular packages on NPM are built using Express. So today we are going to learn how to use this in our web app! This tutorial assumes you have node installed, if you dont visit this [link][nodeInstall].

## Install and Setup
First step is to setup your environment.  Make sure to create a new project directory for this sample app by doing: `$ mkdir basic-routing-example` ( I will be using *basic-routing-example*, but you can use whatever name you would like).  Enter that directory using:

 `$ cd basic-routing-example`
 
 Now that you are in that directory, create a file for our code called *server.js*.  This is the entry point of our application.  Now you need to install the Express.js pacakge with the command:
 
 `$ npm install express --save`
 
 Then if you are familar with Node.js development, we need to create a package.json file using the command:
 
 `$ npm init`
 
 Now that you are all setup to use express time to start coding!

## Code

Open the server.js file we created earlier, and start editing it by adding this to the top of your file:

```
const express = require('express')
const app = express()
var port = 3000
```

The first line allows us to use the Express.js package in our code.  The second line creates a variable called app that is an instance of express.  This is how we will access the functionalities of express.  Then we create a variable called port to store the port the server will listen to when it is started. Then below our variables, add this:

```
app.get('/', function (req, res) {
  res.send('This is our home page!')
})

app.listen(port, function () {
  console.log('We are listening on port ' + port)
})
```

The first bit here is our first example of handling a route.  It is saying that we would like to handle a HTTP `GET` request method on the route `/`, which in this case is the homepage of our web application.  If there is a GET request to the route `/` then it will handle it by calling the callback function specified.  So upon receiving a GET request, it will send a response to the page with the text `This is our home page!`.  In to get this to show we need to have our server listen on a port.  We do that with the second bit of code: `app.listen()`.  To test that you have handled this request properly, save the file, and in the command line enter:
`$ node server.js`.

The command line should output:
`We are listening on port 3000`

Then go to your web browser and enter the page:
`localhost:3000`.
Here is a sample image of what you should see on that page:

![GET_reqImage]()

Now lets test this with a second web page for your web application. Suppose you had an About page as part of your site.  The route you would want for this page would be `/about`.  Lets see how we would handle a GET Request to that page!

```
app.get('/about', function (req, res) {
  res.send('This is a basic app with routing in express')
})
```

This is similar to how we handled the GET request for the home page route of `/`.  Here we change the route to `/about` to specify the About page of our application and we change how we would like to handle it by changing the message being sent in `res.send()`.  Now lets test to see if this works by saving our file, running it with: 
`$ node server.js` and then opening up a web browser and going to the url : `localhost:3000/about`.  This image is what your webpage should look like:

![GET_aboutImage]()

Lets say you wanted to handle another request such as a POST request.  We would add this code to our application:

```
app.post('/', function (req, res) {
  res.send('we got a POST req from the client')
})
```

This handles a `POST` request on the route `/`.  To make this fully functional we would have to go out of the scope of this tutorial, but this is simply an example how you would handle a different type of HTTP request for a route.  

Now what if you had multiple types of HTTP request methods that need to be handled for one route? We could use `app.route()`.  Add this following code snippet and remove your `app.get('/')` and `app.post('/')` handlers :

```
app.route('/')
  .get(function (req, res) {
    res.send('This is our home page!')
  })
  .post(function (req, res) {
    res.send('we got a POST req from the client')
  })
```

This allows us to handle multiple types of HTTP requests for one specific route.  In this case the route is `/` and it has a handler for a `GET` and `POST` request.  

## Conclusion 

You made it! You now have a simple web app that can handle different HTTP request methods on different routes ! Here is a high level overview of what we did here:

1. We installed Express.js
2. Created an instance of Express in our code called app
3. Used that instance to handle multiple routes
4. Used that instance to handle different types of HTTP requests
5. Learned how to use app.route() to simplify handling of HTTP requests for one route.

If you enjoyed this post share it on [twitter][twit]. Check out the code for this tutorial on [GitHub][gitRepo]. 

## Possible Resources

Check out my [GitHub][mainGit]

View my personal [blog][pblog]

Check out [Express.js][expressjs]


[nodeInstall]:  https://nodejs.org/en/download/
[twit]: https://twitter.com/
[gitRepo]: https://github.com/acucciniello/basic-routing-express
[mainGit]: https://github.com/acucciniello/
[expressjs]: http://expressjs.com/
[pblog]: http://www.acucciniello.com/