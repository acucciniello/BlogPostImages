# How to Add an Intent to Your Amazon Echo Skill

## Introduction

If you are new to Amazon Echo Development and have no idea what an Intent is, you have made it to the right place.  What is a intent you ask? It is basically a way for your skill to know what to do when you say a specific phrase to your Amazon Echo.  For example, If I said *"Alexa, ask Greeter to say goodbye"* and I wanted Alexa to respond with *"Goodbye"*,  I would create an intent that handles what the echo does (and ultimately how it responds) when it hears the phrase I gave it.  Without adding your own intents, the echo skill would not be able to handle the different functions you would like it to.  Now this involves two different forms of work, one in your Amazon Developer Portal and the other in your code.

## Developer Portal

First, we should talk about the Developer Portal work.  There are two different parts to setting up your Developer Portal for an intent.

#### Intent Schema

When you are logged in to the Developer Portal for your skill, on the left hand side go to the Interaction Model Section.  Now go to the **Intent Schema** Section.  Your Intent Schema is basically where you create your intents in JSON Format for Alexa to understand them. For a basic example we will be creating an intent called *HelloWorldIntent*.  

![HelloWorldIntentImage](https://github.com/acucciniello/BlogPostImages/blob/master/How-To-Add-Intent-To-Amazon-Echo-Skill/hello-world-intent.png)

Once your Intent Schema looks like this you have now added a new intent to your project.  In order for Alexa, to know when you want to select this intent, you need to add Sample Utterances.

#### Sample Utterances

If you scroll down to the bottom of the page we were on to edit the Intent Schema.  You will see a section called **Sample Utterances**.  A Sample Utterance is a bunch of example phrases that a user would use to invoke this specific intent.  This is how Alexa takes what you say and knows what to do with it.  For example, we could add the statements in this image as Sample Utterances for our HelloWorldIntent.  

![HelloWorldSampleUtterance](https://github.com/acucciniello/BlogPostImages/blob/master/How-To-Add-Intent-To-Amazon-Echo-Skill/h-w-samp-utt.png)

The format for this is: IntentName + phrase you would like to say.  So, now when a user is using this skill he can say *"Alexa, ask Greeter to say hello"*.  Now alexa would take that phrase and know what to do with it because you have code to handle each intent.  

## In Code

Up to this point everything you have done has been in the Amazon Developer Portal for your skill.  Now that the boring part is out of the way you can learn how to actually handle the intent's functionality through code.  

#### Intent Function

First Step is to create a file in the projects root directory called *hello-world-intent.js*.  This is going to be a file that contains a function for handling your HelloWorldIntent. Here is what the code should look like for basic handling of the intent.


```
// hello-world-intent.js
module.exports = HelloWorldIntent

function HelloWorldIntent (intent, session, response) {
  var output = 'Hello World'
  response.tell(output)
  return
}
```
If you are familiar with Node.js, you probably know of *module.exports* for allowing the programmer to add code from different files using *require('./fileName.js')*.  This allows us to use the HelloWorldIntent function in our main js file. 

Our function is pretty basic, it takes three parameters: intent, session, and response.  For the purpose of this lesson we will only be using response.  Response allows the user to send multiple types of responses through alexa.  For this example we will be using response.tell(). At the begining of our function we created a basic string that says *"Hello World"* and stored that in a variable called *output*.  Then the line: *response.tell(output)*.  This tells Alexa to respond to the user with "Hello World".  

#### Main file

In your main js file (the one you use AWS Lambda to point to) add the following line in the top section of your file:

```
// main.js
var HelloWorldIntent = require('./hello-world-intent.js')
```

This is why we used *module.exports* before in order to be able to import your HelloWorldIntent function into the main file. 

Now go to the section of your file where you have: **ServiceName.prototype.intentHandlers = {}**.  This is how you connect the work you did in the Developer Portal to the work you did in your code.  To add an intent handler for an intent add a line inside the brackets like this: *'IntentNameInDevPortal' : IntentFunctionCodeName*.  So in the end your code should look like:

```
GreeterService.protoype.intentHandlers = {
  'HelloWorldIntent' : HelloWorldIntent
}
```

## Conclusion 

Congrats! You have just added your first intent from scratch.  To summarize what happens with your skill from start to finish when invoking an intent here is a quick breakdown:

1. The user says "Alexa, ask Greeter to say hello"
2. Alexa listens to what you are saying
3. She takes the words you said and tries to figure out what to do with them by comparing them to Sample Utterances for the intents you have created
4. She realizes you are invoking the HelloWorldIntent
5. She now executes the code you have established for a HelloWorldIntent (the code in the HelloWorldIntent Function
6. She responds with "Hello World"


## Possible Resources

Use my skill here: [Edit Docs](https://www.amazon.com/Antonio-Cucciniello-Edit-Docs/dp/B01MYOGRD5/ref=sr_1_1?s=digital-skills&ie=UTF8&qid=1482104150&sr=1-1&keywords=edit+docs)

Check out the Code for my skill on [GitHub](https://github.com/acucciniello/alexa-open-doc)

[Alexa Skills Kit Custom Interaction Model Reference](https://developer.amazon.com/public/solutions/alexa/alexa-skills-kit/docs/alexa-skills-kit-interaction-model-reference)

[Implementing the Built-in Intents](https://developer.amazon.com/public/solutions/alexa/alexa-skills-kit/docs/implementing-the-built-in-intents)



