# How to Add Custom Slot Types to Intents

## Introduction
Have you created an Intent where you wanted to add your own slot types to it? If this is you, hopefully after following this guide you should be on your way to creating as many custom slot types as you like.  

Before we go any farther, let us define what a *slot* is in Amazon Echo Skill Development.  A slot essentially is a way to access what the user says when requesting something and then using it in your code to execute the skill's functionality properly. For example, lets say I created a skill that repeated a name back to me, and the request was "Alexa, ask Repeater to respond with John".  Alexa would then respond with "John".  In this case the slot value would be John.  In order to make slots we need to do a couple of things in our Developer Portal and in our code.

## Amazon Developer Portal

First, we will visit the steps to implement a slot in your Developer Portal.  There are three individual parts to this.

#### Intent Schema
Once you have logged in to your Developer Portal for the skill you would like to add a slot to, click on Interaction Model tab on the left hand side.  Go to the **Intent Schema** section.  This is a JSON object that holds all of your intents.  Here we are going to create a new intent to our skill.  For example, if our skill's name was Repeater and we wanted Alexa to respond with a name the user said back to them, our intent schema would look like this:

```
{
  "intents": [
    {
      "intent": "RepeatNameIntent",
        "slots": [
          {
            "name": "repeatName",
            "type": "REPEAT_NAME"
          }
    }
  ]
}
```

Here we specify the intent name as *RepeatNameIntent*, then specify that the intent will have one slot named *repeatName* that is of the custom slot type *REPEAT_NAME*.  Now we have created an intent for Alexa to handle while using this skill.  It is now time to define what the custom slot type of *REPEAT_NAME* is.

#### Custom Slot Types

Now that the intent has been added, in order to define the custom slot type of *REPEAT_NAME*, scroll down to the *Custom Slot Type* section. Now click on *Add Slot Type*.  Enter the type as the same type you made in your Intent Schema (for this example we will create it of type *REPEAT_NAME*).  Then it will ask you to enter values.  Here Amazon is looking for example things a user would say for this slot, in order to know when the slot is being used.  In the case of the *REPEAT_NAME* I have placed a bunch of different names as values for Alexa to handle.  Here is an image of the custom slot type with its values:

![REPEAT_NAMESlotImage](https://github.com/acucciniello/BlogPostImages/blob/master/How-To-Add-Custom-Slot-Types-to-Intents/REPEAT_NAME-Slot.png)

#### Sample Utterances

Once you have defined what your custom slot type will look like by giving it Sample Values, it is time to create a couple of Sample Utterances so the skill knows where the slot type will be when invoking the intent.  In order to specify where the slot will be in the Sample Utterance, you must use the format: {nameOfSlot}. 

For example, here are a couple of Sample Utterances I implemented for the RepeatNameIntent:

```
RepeatNameIntent to repeat the name {repeatName}
RepeatNameIntent to say the name {repeatName}
RepeatNameIntent to respond with the name {repeatName}

```

Now, by giving these Sample Utterances, Alexa knows that what the user says after the word "name" in the skill is what you would like repeated back to you.  In order to implement this, we need to access the slot in our code.

## Code

Now that you have the logistics of setting up the intent and custom slot type in your Developer Portal, you can move on to implementing the intent's functionality. 

```
// repeat-name-intent.js
module.exports = RepeatNameIntent

function RepeatNameIntent (intent, session, response) { 
  var name = intent.slots.repeatName.value
  response.tell(name)
  return
}
```

The way to access the value of what the user is saying is through *intent.slots.slotName.value*.  For your skill you would replace slotName with the actual name of the slot that you used in your Intent Schema in the Developer Portal. For this example, we accessed the value and stored it in a variable called name and then had Alexa respond with the name to the user.

Now to make sure that you have the intent being handled in your code, head over to your main js file for this skill (the file where AWS Lambda is pointing to). Add the following line to pull in your intent function into your main file:

```
// main.js 
var RepeatNameIntent = require('./repeat-name-intent.js')
```

Once you have added that line, you can add this next line in your intentHandlers in order for your skill to know which intent in your Developer Portal's intent schema relates to which function in your code:

```
RepeaterService.protoype.intentHandlers = {
  'RepeatNameIntent' : RepeatNameIntent
}
```

This takes the form of **'IntentNameInDevPortal' : IntentNameInCode**.  

## Conclusion

If you have made it this far, you have successfully added a custom slot type to your Intent! I will briefly explain what happens when invoking the skill with your custom slot type:

1. The user says "Alexa, ask Repeater to say the name Joe"
2. Alexa listens to what you are saying
3. She recognizes that you are invoking the RepeatNameIntent and saying the slot should be "Joe"
4. She now executes the function RepeatNameIntent because your intent handler tells her that is how you would like to handle that intent.
5. She responds with "Joe"


## Possible Resources
Use my skill here: [Edit Docs](https://www.amazon.com/Antonio-Cucciniello-Edit-Docs/dp/B01MYOGRD5/ref=sr_1_1?s=digital-skills&ie=UTF8&qid=1482104150&sr=1-1&keywords=edit+docs)

Check out the Code for my skill on [GitHub](https://github.com/acucciniello/alexa-open-doc)

[Alexa Skills Kit Custom Interaction Model Reference](https://developer.amazon.com/public/solutions/alexa/alexa-skills-kit/docs/alexa-skills-kit-interaction-model-reference)

[Migrating to the Improved Built-in and Custom Slot Types](https://developer.amazon.com/public/solutions/alexa/alexa-skills-kit/docs/migrating-to-the-improved-built-in-and-custom-slot-types)