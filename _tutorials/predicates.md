---
layout: default
title: Predicates 101
---

# Predicates 101: Customize your bot's conversation

This tutorial will help you understand how to customize your bot's conversation for each of your end-users.

First, you will step through some simple AIML code, to explain how predicates (and other AIML variables) are used for this feature. Next, API requirements for identifying each end-user are covered.


# AIML 

## What are variables in AIML?

In programming, a variable is a symbol whose value can be changed; AIML has variables as well. These can be used to store information about your bot, end-user (AKA client), or anything else you would like. There are 4 types:

* Properties - global constants for a bot. Can only be changed by the botmaster.
* Predicates - global variables for the bot. Usually set by the client when a template is activated.
* Local variables - which are just like predicates, except their scope is limited to one category.
* System built ins - `that` and `topic` are special type of variable that are usually set by the client when a template is activated. Note that these values are only valid during an active conversation, and are not persistent.

### Using Properties
For example, you can use a property to store your bot's age. Create a new property with the name "age" and the value "8" in your bot's properties file**. Then insert this category:

    <category>
    <pattern>HOW OLD ARE YOU</pattern>
    <template>I am <bot name="age" /> years old.</template>
    </category>

*Human*: How old are you?  
*Bot* : I am 8 years old.

Since this is a bot property, any client entering in this input will receive the same response. And since it is a constant, it can only be changed by updating the bot properties file, uploading the file, and re-compiling your bot.
 
**Note that a default bot properties file is automatically created when you create a bot on Pandorabots bot hosting platform. Bot properties file format is a key/value pair array (see [Rosie example](https://github.com/pandorabots/rosie/blob/master/lib/system/rosie.properties) for format).

### Setting and Recalling Predicates 

Using a predicate variable, you can write a category that will store, for example, the name of your client. This category will store the client's name under a predicate called "name":

    <category>
    <pattern>MY NAME IS *</pattern>
    <template>Nice to meet you, <set name="name"><star /></set></template>
    </category>

Note how the user of the * wildcard and `<star />` tag allows you to write a single category that will capture any name!

Once you have set a predicate, it can be recalled elsewhere in your AIML.

    <category>
    <pattern>WHAT IS MY NAME</pattern>
    <template>Your name is <get name="name" />.</template>
    </category>

If you have set the predicate using the previous category, this will now recall the value of the predicate "name". If the predicate has **not** been set, then your bot will return the `default-get` value specified in your bot properties file. For example, in Rosie, it is set to "unknown".

The categories you have just written would enable a conversation like the one below:

*Human:* My name is Daniel.  
*Bot:* Nice to meet you, Daniel.  

*Human:* What is my name?  
*Bot:* Your name is Daniel.

### Using var
Local variables work almost exactly like predicates, but their scope is limited to a single category. These are different from predicates, which can be recalled later in a conversation. Typically you would want to use this in some internal AIML coding not for the client to see.

Let's say you don't want your bot to return "Your name is unknown." in the case of a client asking without actually telling the bot their name. You can introduce the `<condition>` tag using a local variable called `checkname`, such as:

    <category>
    <pattern>WHAT IS MY NAME</pattern>
    <template>
       <think><set var="checkname"><get name="name" /></set></think> 
       <condition name="checkname">
         <li value="unknown">You haven't told me your name yet!</li>
         <li>Your name is <get var="checkname" />.</li>
       </condition>
    </template>
    </category>

Set the local variable to the value of the predicate `name` and use the `<condition>` tag to control the bot response. Once this interaction has been completed, `checkname` will no longer have a value associated with it. 


### AIML Reference links
For more about the AIML tags used in this tutorial, please see the following AIML references:  
 [condition](http://docs.pandorabots.com/aiml/condition/)   |   [get](http://docs.pandorabots.com/aiml/get/)   |  [li](http://docs.pandorabots.com/aiml/li/)  |  [set](http://docs.pandorabots.com/aiml/set/)  |  [think](http://docs.pandorabots.com/aiml/think)


# API


## Saving predicates per clients using talk API
Now you have AIML code in your bot to set and retrieve predicates based on client (AKA end-user) talking to your bot. 

In order to save a different value per client, in your application, when you use the [Talk to a Bot API](https://developer.pandorabots.com/docs#!/pandorabots_api_swagger_1_3/talkBot) you must provide a `client_name` parameter in the talk request that is unique to each client.  Without a valid `client_name` parameter, predicates will be associated to your Pandorabots app_id, causing unexpected responses. For example: User A says her name is Amy, User B then says his name is Ben. Then if both (or any) users ask what their name is, your bot will respond with the last predicate value saved, which would be Ben).

If your bot is talking to random strangers that you want to be able to retain predicates only during an active conversation, but not long-term, you can create a random (but unique) value within your application that conforms to the `client_name parameter` format. For example, any number of 3-64 digits is a valid format so a random number generator starting at 100 could be a simple solution for your application. A random string generator could also work, as long as it conforms to the parameter format. 

As long as the end-user is in an active conversation, all predicates that were set during the chat are preserved and can be recalled. As soon as the end-user stops interacting with the bot for an extended idle period (typically 30-40 minutes), their predicates will be cleared from bot memory.


## Saving persistent predicates for clients using Anonymous Talk API

If you want your bot to retain conversational elements long term, regardless if they are anonymous users, or known end-users, this can be achieved by requesting a Pandorabots generated client_name with the anonymous talk API.

Please review this article about [Anonymous Talk API](http://docs.pandorabots.com/articles/managing-end-users-with-a-talk/) for more details.
