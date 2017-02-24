# How to use XmlHttpRequests to Send POST to Server

## Introduction

So, you need to send some bits of information from your browser to the server in order to complete some processing.  Maybe you need the information to search for something in a database, or just to update something on your server.  Today I are going to show you how to send some data to your server from the client through a POST request using *XmlHttpRequest*.  First, we need to set up our environment!

## Set up

The first thing to make sure you have is [Node and NPM][nodeInstall] installed.

Create a new directory for your project, here we will call it **xhr-post**:

```
$ mkdir xhr-post
$ cd xhr-post
```

Then we would like to install *express.js* and *body-parser*:

```
$ npm install express
$ npm install body-parser
```

Express makes it easy for us to handle HTTP requests, and body-parser allows us to parse incoming request bodies.  Let's create two files one for our server called *server.js* and one for our front end code called *index.html*.  Then initialize your repo with a package.json file by doing:

`$ npm init`

## Client

Now its time to start with some front end work.  Open and edit your `index.html` file with:

```
<!doctype html>
  <html>
    <h1>
    XHR POST to Server
    </h1>
    <body>
      <input type='text' id='num' />
      <script>
        function send () {
          var number = {
            value: document.getElementById('num').value
          }
          var xhr = new window.XMLHttpRequest()
          xhr.open('POST', '/num', true)
          xhr.setRequestHeader('Content-Type', 'application/json;charset=UTF-8')
          xhr.send(JSON.stringify(number))
        }
      </script>
      <button type='button' value='Send' name='Send' onclick='send()' >
        Send
      </button>
    </body>
  </html>
```

This file simply has a input field to allow users to enter some information, and a button to then send the information entered to the server.  What we should focus on here is the button's onclick method `send()`.  

This is the function that is called once the button is clicked.  We create a JSON object to hold the value from the text field. Then we create a new instance of an XMLHttpRequest with `xhr`.  We call `xhr.open()` to initialize our request by giving it a request method (POST), the url we would like to open the request with ('/num') and determine if it should be asynchronous or not (set `true` for asynchronous).

We then call `xhr.setRequestHeader()`.  This sets the value of the HTTP request to json and UTF-8.

As a last step, we send the request with `xhr.send()`.  We pass the value of the text box and stringify it to send the data as raw text to our server, where it can be manipulated there. 

## Server

Here our server is supposed to handle the POST request and we are simply going to log the request received from the client.  

```
const express = require('express')
const app = express()
const path = require('path')
var bodyParser = require('body-parser')
var port = 3000

app.listen(port, function () {
  console.log('We are listening on port ' + port)
})

app.use(bodyParser.urlencoded({extended: false}))
app.use(bodyParser.json())

app.get('*', function (req, res) {
  res.sendFile(path.join(__dirname, '/index.html'))
})

app.post('/num', function (req, res) {
  var num = req.body.value
  console.log(num)
  return res.end('done')
})
```

At the top, we declare our variables, obtaining an instance of express, path and body-parser.  Then we set our server to listen on port 3000. 

Next, we use `bodyParser` object to decide what kind of information  we would like to parse, we set it to json because we sent a json object from our client if you recall the last section. This is done with:

`app.use(bodyParser.json())`

Then we serve our html file in order to see our front end that we created in the last section with:

```
app.get('*', function (req, res) {
  res.sendFile(path.join(__dirname, '/index.html'))
})
```

The last part of server.js is where we handle the POST request from the client.  We access the value sent over by checking for corresponding property on the body object which is part of the request object.  Then as a last step for us to verify we have the correct information, we will log the data received to the console and send a response to the client.

## Test

Let's test what we have done.  In the project directory we can run: 

`$ node server.js`

Open your web browser and go to the url `localhost:3000`.  This is what your web page should look like:

![XHRclient_Image](https://github.com/acucciniello/BlogPostImages/blob/master/XHR-to-Send-POST-Request-to-Server/XHRclient.png)

This is what your output to the console should look like if you enter a 5 in the input field:

![Console_Image](https://github.com/acucciniello/BlogPostImages/blob/master/XHR-to-Send-POST-Request-to-Server/Console.png)

## Conclusion 


You are all done! You now have a web page that sends some JSON data to your server using XmlHttpRequest! Here is a summary of what we went over:

1. Created a Front End with an input field and button
2. Created a function for our button to send an XmlHttpRequest
3. Created our server to listen on port 3000
4. Served our html file
5. Handled our POST request at route `'/num'`
6. Logged the Value to our Console

If you enjoyed this post share it on [twitter][twit]. Check out the code for this tutorial on [GitHub][gitRepo]. 

## Possible Resources

Check out my [GitHub][mainGit]

View my personal [blog][pblog]

Information on [XmlHtttpRequest][XHR]

GitHub pages for:

 [express][express]
 
 [body-parser][bodyParser]


[twit]: https://twitter.com/
[gitRepo]: https://github.com/acucciniello/client-redirecting-react-router
[mainGit]: https://github.com/acucciniello/
[pblog]: http://www.acucciniello.com/
[nodeInstall]: https://nodejs.org/en/download/
[XHR]: https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest
[bodyParser]: https://github.com/expressjs/body-parser
[express]: https://github.com/expressjs/express