# What is the Difference Between Functional and Object Oriented Programming?## Introduction

There are two very popular programming paradigms in software development that developers design and program to.  They are known as Object Oriented Programming and Functional Programming.

I am sure you have heard of these terms before but what exactly are they and what is the difference between the two paradigms?  Today I hope to answer just that for you!

## Object Oriented Programming
Object Oriented Programming is a programming paradigm in which you program using objects to represent things you are programming about (sometimes real world things).   These objects could be data structures.  The objects hold data about them in attributes.  The attributes in the objects are manipulated through methods or functions that are given to the object.

For instance, we might have a Person object that represents all of the data a person would have: a weight, height, skin color, hair color, hair length, and so on.  Those would be the attributes.  Then the person would also have things it can do such as: pick box up, put box down, eat, sleep.  These would be the functions that play with the data the object stores.

Engineers who program using Object Oriented design say that it is a style of programming that allows you to model real world scenarios much simpler.  This allows for a good transition from requirements to code that works like the customer or user wanted it to.

Some examples of Object Oriented Languages would be C++, Java, Python, C#, Objective-C, and Swift.  ## Functional Programming

Functional Programming is the form of programming that attempts to avoid changing state and mutable data.  In a functional program the output of a function should always be the same, given the same exact inputs to the function.

This is because the outputs of a function in functional programming purely relies on arguments of the function and there is no magic that is happening behind the scenes.  This is called eliminating side effects in your code.

For example, if you call function `getSum()`.  It calculates the sum of two inputs and returns sum.  Given the same inputs for `x` and `y`, we will always get the same output for `sum`.

This allows the function of a program to be extremely predictable.  Each small function does its part and only its part.  It allows for very modular and clean code that all works together in harmony.  This is also easier when it comes to unit testing.

Some examples of Functional Programming Languages would be Lisp, Clojure, and F#.

## Problems with Object Oriented Programming

There are a few problems with Object Oriented Programing.  First, it is known to be not as reusable.  Since some of your functions depend on the class that is using them it is hard to use some function with another class.

It is also known to be typically less efficient and more complex to deal with.  Plenty of times, Object Oriented designs are made to model large architectures and can be extremely complicated.
## Problems with Functional Programming

Functional Programming is not without its flaws either.  First, it really takes a different mindset to approach your code from a functional standpoint.  Its is easy to think in Object Oriented terms because it is similar to how the object being modeled happens in the real world. Functional programming is all about data manipulation.  Converting a real world scenario to just data can take some extra thinking.

Due to its difficulty when learning to program this way, there are fewer people that program using this style.  Which could make it hard to collaborate with someone else or learn from others as there will naturally be less information on the topic.
## Comparing Both

Both programming concepts have a goal of wanting to create easily understandable programs that are free of bugs and can be developed fast.  Both concepts have different methods for storing the data and how to manipulate the data.  In Object Oriented Programming, you store the data in attributes of objects and have functions that work for that object and do the manipulation.  In Functional Programming, we view everything as data transformation.  Data is not stored in objects, it is transformed by creating new versions of that data and manipulating it using one of the many functions.

## Conclusion I hope after reading this, you have a clearer picture of what the difference is between Object Oriented programming and Functional programming paradigms.  They can both be used separately or can be mixed to some degree to suite your needs.  Ultimately you should take into the consideration the advantages and disadvantages of using both before making that decision!If you enjoyed this post share it on [twitter][twit]! Tweet at me with your favorite of the oldest languages that are still in use.  
## Possible ResourcesCheck out my [GitHub][mainGit]View my personal [blog][pblog]Check out my YouTube [Channel][youtube][twit]: https://twitter.com/[mainGit]: https://github.com/acucciniello/
[pblog]: http://www.acucciniello.com/
[youtube]: https://www.youtube.com/channel/UC8icMMql5SjCaXXMvILGIUA