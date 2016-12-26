# How to Add Custom Slot Types to Intents

## Introduction
Have you created an Intent where you wanted to add your own slot types to it? If this is you, hopefully after following this guide you should be on your way to creating as many custom slot types as you like.  

Before we go any farther, let us define what a *slot* is in Amazon Echo Skill Development.  A slot essentially is a way to access what the user says when requesting something and then using it in your code to execute the skill's functionality properly. For example, lets say I created a skill that repeated a name back to me, and the request was "Alexa, ask Repeater to respond with John".  Alexa would then respond with "John".  In this case the slot value would be John.  In order to make slots we need to do a couple of things in our Developer Portal and in our code.

## Amazon Developer Portal

First, we will visit the steps to implement a slot in your Developer Portal.  There are three individual parts to this.

#### Intent Schema
Once you have logged in to your Developer Portal for the skill you would like to add a slot to, click on Interaction Model tab on the left hand side.  Go to the **Intnet Schema** section.  This is a JSON object that holds all of your intents.  Here we are going to create a new intent to our skill.  For example if our skill's name was Repeater and we wanted Alexa to respond with a name the user said back to them, our intent schema would look like this:

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

Here we specifiy the intent name as *RepeatNameIntent*, then specifiy that the intent will have one slot named *repeatName* that is of the custom slot type *REPEAT_NAME*.  Now we have created an intent for Alexa to handle while using this skill.  It is now time to define what the custom slot type of *REPEAT_NAME* is.

#### Custom Slot Types

Now that the intent has been added, in order to define the custom slot type of *REPEAT_NAME*, scroll down to the *Custom Slot Type* section. Now click on *Add Slot Type*.  Enter the type as the same type you made in your Intent Schema (for the sake of the example we will create it of type *REPEAT_NAME*).  Then it will ask you to enter values.  Here Amazon is looking for example things a user would say for this slot, in order to know when the slot is being used.  In the case of the *REPEAT_NAME* I have placed a bunch of different names as values for Alexa to handle.  Here is an image of the custom slot type with its values:

![REPEAT_NAMESlotImage]()

#### Sample Utterances

## Code

## Conclusion

## Possible Resources
Use my skill here: [Edit Docs](https://www.amazon.com/Antonio-Cucciniello-Edit-Docs/dp/B01MYOGRD5/ref=sr_1_1?s=digital-skills&ie=UTF8&qid=1482104150&sr=1-1&keywords=edit+docs)

Check out the Code for my skill on [GitHub](https://github.com/acucciniello/alexa-open-doc)

[Alexa Skills Kit Custom Interaction Model Reference](https://developer.amazon.com/public/solutions/alexa/alexa-skills-kit/docs/alexa-skills-kit-interaction-model-reference)

[Migrating to the Improved Built-in and Custom Slot Types](https://developer.amazon.com/public/solutions/alexa/alexa-skills-kit/docs/migrating-to-the-improved-built-in-and-custom-slot-types)