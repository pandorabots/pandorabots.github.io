---
layout: integrations
title: Hubot
---

# Putting your bot on #Slack

In this week's tutorial, we'll be revisiting [Firebase](https://firebase.com), this time as a way to store the conversations that users are having with a chatbot. We'll be using jQuery and Twitter Bootstrap to create a responsive, real time interface that will also allow you to track conversations as they are happening.

##  The code

In our previous post on [Bot Possession](http://blog.pandorabots.com/bot-possession/), we explored Firebase as a tool to generate different types of events that would cause our interfaces to respond in different ways. In this post, we'll be using it more like a traditional database, with the added benefit of a responsive interface to track new conversations in real time.

**Setup**

You can grab the source code for this tutorial from its [repository on Github](https://github.com/pandorabots/pb-logs-firebase):

```
$ git clone https://github.com/djfdev/pb-logs-firebase.git
$ cd pb-logs-firebase
```

We'll be using the command line utility [Bower](http://bower.io/) to manage our dependencies (Bower requires node.js, npm, and Git):

```
$ npm install -g bower
$ bower install
```

If you haven't already, create an account on Firebase along with a new application. Grab the URL of the application and insert it into both `js/user.js` and `js/log.js` as the `root` variable:

```
...
var root = "https://your-firebase.firebaseio.com/";
...
```

You'll also need to include your Pandorabots API credentials in `js/user.js`:

```
...
var pb = new Pandorabot("aiaas.pandorabots.com", APP_ID, BOTNAME, USER_KEY);
...
```

Because the Pandorabots web client requires cookies, you'll have to either enable file cookies in your browser, or host the files on a server.

**Chat interface**

![](/content/images/2014/11/Screen-Shot-2014-11-14-at-12-18-38-PM.png)

The chat interface is very similar to the one we used in the Bot Possession tutorial, however, our Javascript is handling each interaction a bit differently. We're relying heavily on the `sessionid` that Pandorabots uses to identify conversations. If no `sessionid` is passed in the the Talk API, then Pandorabots will return one in the response that can be passed in to subsequent requests.

The `sessionid` is distinct from the `client_name` used to identify your users. While each user has a single unique `client_name`, they may have many different sessions (implying that they have had multiple conversations with the same bot).

**Talk logs page**

![](/content/images/2014/11/Screen-Shot-2014-11-14-at-12-18-51-PM.png)

This page will display new conversations as they are initialized when end users open a new chat interface. Each row of the table represents a new conversation, identified by a timestamp, `client_name`, and `sessionid`. Clicking on a `sessionid` will open a modal dialog with the contents of that conversation.

![](/content/images/2014/11/Screen-Shot-2014-11-14-at-12-19-00-PM.png)

Because we have attached event listeners for each individual conversation, new interactions will be displayed in the modal as they arrive.

##  Back to Firebase

While this interface provides a clean, simple way for you to track your bot's talk logs, you can actually export your entire Firebase as JSON data for further use and analysis. The data structure we've constructed here makes it very easy to work with. Here's the JSON extracted for the above conversation:

```
{
  "8229" : {
    "client_name" : "297014",
    "conversation" : {
      "-Ja_arxLSeKakX6QhSuX" : {
        "client_name" : "297014",
        "date" : "Wed Nov 12 2014 12:04:31 GMT-0800 (PST)",
        "input" : "Hello",
        "response" : [ "Hi it's great to see you!" ],
        "that" : ""
      },
      "-Ja_iNPY2TM14Z_N246U" : {
        "client_name" : "297014",
        "date" : "Wed Nov 12 2014 12:37:19 GMT-0800 (PST)",
        "input" : "How are you?",
        "response" : [ "I'm very well. How are you doing?" ],
        "that" : "Hi it's great to see you!"
      }
    },
    "date" : "Wed Nov 12 2014 12:04:31 GMT-0800 (PST)"
  }
}
```

Both the session and each individual interaction have a `date` and `client_name` for ease of use.

##  Talk logs and Zipf's Law

The importance of your bot's talk logs in the bot development process goes back to a statistical trend named after American linguist George Kingsley Zipf. Zipf's law explains how the frequency of certain words in natural languages relate to each other:

>Zipf's law states that given some corpus of natural language utterances, the frequency of any word is inversely proportional to its rank in the frequency table. Thus the most frequent word will occur approximately twice as often as the second most frequent word, three times as often as the third most frequent word, etc.  
- *[Wikipedia](http://en.wikipedia.org/wiki/Zipf's_law)*

Dr. Richard Wallace, the creator of Alicebot and inventor of AIML, discerned that this applied not only to individual words, but to phrases as well. This distribution pattern led to a key insight in chatbot development. By writing patterns and content to capture only the most common inputs being used, the developer could actually account for the majority of potential inputs.

>Specifically, 1800 words cover 95% of all the first words input to ALICE.  
- *[Dr. Richard Wallace](http://www.alicebot.org/articles/wallace/zipf.html)*

(Note that the [Rosie Framework](https://github.com/pandorabots/rosie) is a product of this invaluable conversational data, designed to save developers from hacking away by blindly guessing what end-users might say.)

By keeping a close eye on your talk logs, you can gather similar data about your own bot. This will provide insight about the inputs that are the most important for your bot to understand given the context and domain in which your bot is being used. Keep in mind that the best bots are often **domain specific** -- and that designing a bot to be an expert on a particular topic or domain leads to a far higher rate of successful interactions. Once you've implemented the conversation tracking features outlined in this tutorial, you can start collecting the data needed to run your own Zipf's analysis and truly make your bot a master of its own domain.
