# The 5 Worst Things about JavaScript## IntroductionIf you are new to JavaScript, you may find it a little confusing depending on what language you came from.  Although JavaScript is my favorite language to use today, I cannot say that it was always this way.  There were some things I truly despised and was genuinely confused with in JavaScript.  At this point I have come to accept these things. Today we will discuss the five worst things about the JavaScript programing language.

## Global VariablesNo matter the programming language you are using, it is never a good idea to have variables, functions, or objects as part of your global scope.  It is good practice to limit the amount of global variables as much as possible.  

As programs get larger there is a greater chance of naming collisions and giving access to code that does not necessarily need it by making it global.  When implementing things, you would want a variable to have a large enough scope as you need it to be.  

In JavaScript, you can access some global variables and objects through `window	`.  You can add things to this if you would like but you should not do this.
## Use of Bitwise Operators

As you probably know, JavaScript is a high level language that does not communicate with the hardware much.  There are these things called Bitwise Operators that allow you to compare the bits of two variables.  For instance `x & y` does an AND operation on x and y.  The problem with this is in JavaScript there is no such thing as integers only double precision floating point numbers.  So in order to do the bitwise operation, it must convert x and y to integers, compare the bits, and then convert them back to floating point numbers.

This is much slower to perform and really should not be done, but then again it is some how allowed.

## Coding Style Variations

From seeing many different open source repositories, there does not seem to be one Coding Style Standard that everyone adheres too.  Some people love semicolons, others hate them.  Some people adore ES6, other people despise it.  

Personally I am fan of using Standard for coding style, and use ES5.  That is soley my opinion though.  When comparing code to other people who have completely different styles, it can really be difficult attempting to use their code or write something similar to them.  

It would be nice to have a more generally accepted style that is used by all JavaScript developers. It would make us overall more productive.## Objects

Coming from a Class based language, I found the topic of prototypical  inheritance difficult to understand and use.  In prototypical inheritance all objects inherit from `Object.prototype`.  That means that if you try to refer to a property of an object that you have not defined for yourself, but exists as part of `Object.prototype` then it will execute using that property or function.  

There is a chain of objects where each object inherits all of the properties from its parent and all of that parents' parents.  Meaning your object might have access to plenty of functions it does not need. Luckily you can override any of the parent functions by establishing a function for this object.
## Large Amount of Falsy Values

Here is a table of falsy values that are used in JavaScript: 

| False Value | Type      |
|-------------|-----------|
| 0           | Numbers   |
| NaN         | Numbers   |
| ''          | String    |
| false       | Boolean   |
| null        | Object    |
| undefined   | undefined |

All of these values represent a different falsy value but they are not interchangeable.  They only work for their type in JavaScript.  As a beginner, trying to figure out how to check for errors at certain points in your code, sometimes this can be tricky.

Not to harp on the problem with global variables again, but `undefined` and `NaN` are both variables that are part of global scope.  This means that you can actually edit the values of them.  Which should be illegal, cause this one change can affect your entire product or system.
## Conclusion As mentioned in the beginning, this is simply my opinion.  I am coming from a background in C/C++ and then started learning JavaScript.  These were the top 5 problems I had with JavaScript that made me really scratch my head.  You might have a completely different opinion reading this from your different technical background.  I hope you share your opinion!
If you enjoyed this post share it on [twitter][twit]! Tweet at me with your about least favorite part of using JavaScript. If you love JavaScript and think its perfect, I would love to hear from you as well!  
## Possible ResourcesCheck out my [GitHub][mainGit]View my personal [blog][pblog]Check out my YouTube [Channel][youtube][twit]: https://twitter.com/[mainGit]: https://github.com/acucciniello/
[pblog]: http://www.acucciniello.com/
[youtube]: https://www.youtube.com/channel/UC8icMMql5SjCaXXMvILGIUA