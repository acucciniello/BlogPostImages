# How is Node.js Changing Web Development?## Introduction

If you have remotely been paying attention to what is going on in the web development space, you know that Node.js has become extremely popular and many developer's choice of backend technology.  It all started in 2009 by Ryan Dahl.   It is a JavaScript runtime that is built on Google Chrome's V8 JavaScript Engine.Over the past couple of years, more and more engineers have moved towards Node.js in many of the their web applications.  As an affect how has Node.js changed web development?

## ScalabilityScalability is the one thing that makes Node.js so popular.  Node.js runs everything in a single thread.  This single thread is event driven (due to JavaScript being the language that it is written with).  It is also non-blocking.

Now when you spin up a server in your Node web app, every time a new user connects to the server, that launches an event.  That event gets handled concurrently with the other events that are occurring or users that connecting to the server.

In web applications built with other technologies, this would slow down the server after a large amount of users.  In contrast, with a Node application, and the non blocking event driven nature, this allows for highly scalable applications.

This now allows companies that are attempting to scale to build their apps with Node to prevent any slow downs they could have had.  This also means they would not have to purchase as much server space as someone using a web app that was not developed with Node.
## Ease of Use

As I previously mentioned, Node.js is written with JavaScript.  Now JavaScript was always used to add functionality to the frontend of applications.  But with the addition of Node.js, you can now write it the entire application in JavaScript.

This now makes it so much easier to be a frontend developer who can edit some backend code, or be a backend engineer who can play around with some frontend code.  

This now makes it so much easier to become a Full Stack Engineer.  You do not really need to know anything new except the basic concepts of how things work in the backend.  As a result, we have recently seen the rise in a full stack JavaScript developer.  This also reduces the mental context switch when switching from JavaScript on the frontend to whatever language that used to be used on the backend.

## Open Source Community

When Node was released, NPM, node package manager, was also given to the public.  The node package manager does exactly what it sounds like it would do: it allows developers to quickly add and use third party libraries and frameworks in your code.  

If you have used Node then you can vouch for me here when I say, there is almost always a package that you could use in your application that can make it easier to develop your application or automate a larger task.

There are packages to help create http servers, help with image processing, help with unit testing.  You need it its probably made.  The even more awesome part about this community that its growing by the day, and people are extremely active by contributing the many open source packages out there to help developers with various needs.

This increases the productivity of all developers that are using Node in their application because they can shift the focus from something that is not that important in their application, to the main purpose of it.

## Aid in Frontend DevelopmentWith the release of Node it did not only benefit the backend side of development.  It also benefited the frontend.  With new frameworks that could be used on the frontend such as React.js or virtual-dom, these are all installed using NPM.  With packages like `browserify` you can also use Node’s require to use packages on the frontend that normally would be used on the backend!  Now you can be even more productive and develop things faster on the front end as well!## Conclusion 

Node.js is definitely changing web development for the better.  It is making engineers more productive with the use of one language across the entire stack.  So my question to you is, if you have not tried out Node in your application what are you waiting for? Do you not like being more productive?
If you enjoyed this post share it on [twitter][twit]! Tweet at me with your opinion of how Node.js changed web development.  If you dislike Node.js I would love to hear your opinion as well!
## Possible ResourcesCheck out my [GitHub][mainGit]View my personal [blog][pblog]Check out my YouTube [Channel][youtube][twit]: https://twitter.com/[mainGit]: https://github.com/acucciniello/
[pblog]: http://www.acucciniello.com/
[youtube]: https://www.youtube.com/channel/UC8icMMql5SjCaXXMvILGIUA