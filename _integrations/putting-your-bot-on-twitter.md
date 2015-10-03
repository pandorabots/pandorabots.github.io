---
layout: integrations
title: Twitter
---

# Putting your Pandorabot on Twitter

## Introduction
Wouldn't it be cool if you could put your Pandorabot on Twitter? People from all over the world could tweet at your bot, talking to it just as they would if they were chatting with it over the Pandorabots Talk API. Introducing your Pandorabot to Twitter allows your Pandorabot to foster meaningful relationships with Twitter's widespread and diverse user base, interacting on the cutting edge of technology. You already have an entertaining and engaging bot, now you can start building it's following.

## Overview

This blog post walks you through the process of putting your Pandorabot on Twitter. Upon completion of the steps outlined here, your bot will have a dedicated profile on Twitter, and you will have an application that is able to automatically tweet any user that has tweeted your bot. Think of it as using Twitter as a giant chat interface, one that is able to connect a vast amount of new users to your bot. Whatever someone says to your bot’s profile on Twitter will be interpreted, just as it is on the Pandorabots platform, and your bot will then tweet back. Let’s get started!

_This tutorial assumes you have a Pandorabot. If you don't though, don't worry, it is quite easy to build one. Just follow our [Build a Bot Tutorial](https://playground.pandorabots.com/en/tutorial/). Also required is the __user\_key__ you received when you initially deployed your bot. It can be found on your Pandorabots Apllication's page in the [Developer Console](https://developer.pandorabots.com/). For more information on deploying your bot to our server, please see our [previous blog post](http://blog.pandorabots.com/basic-bot-deployment/) on the subject._

## First Steps
The first thing to do is create a Twitter user account for your bot. Go to [Twitter](https://twitter.com/) and do so. You will have to provide a name and an email address, as well as do a few other things to get your account set up. Before creating your Twitter application, return to your email account, where there should be a new message from Twitter asking you to confirm your email address. Do this, and you’re all set to build your Twitter application!

Go to the Twitter [applications site](https://apps.twitter.com). You should still be logged in, but if for some reason you are not, log in with the same user credentials you created for your Twitter account. Click the button labeled __Create New App__. You will be asked to provide a name, description, and website for your app. If you don’t have a website for your Pandorabot, you can use a placeholder url _(e.g. http:_//_www.placeholder.com)_ until you get one. Scroll down to the bottom of the page, read the __“Developer Rules of the Road”__, accept them, and then click the __Create your Twitter Application__ button.

Next you will need to change your application’s access level from _Read only_ to _Read and Write_. Under the heading __Application Settings__, you will see your application’s access level. Click the blue link beside it labeled __modify app permissions__. On the next page, change your application’s access from _Read only_ to _Read and Write_ and click the __Update Settings__ button. It may take a few moments for this change to be reflected on the Twitter site, so don’t fear if the _Read only_ option is still selected initially.

You may be asked to provide a mobile phone number for your application to change its app permissions.  To accomplish this, go back to your bot’s [Twitter homepage](https://twitter.com). Click the gear icon in the upper right hand corner of your homepage, and select the __Settings__ option listed. On the left hand side of the page is a list of setting items, with the __Account__ element selected. Click on the element labeled __Mobile__ and input your information on the following page to activate a phone with the account.

Once this has been completed the next thing to do is generate your _access keys_. Go to your Twitter App [page](https://apps.twitter.com) and select the app you just created. Click the __API Keys__ tab underneath your application’s name. Take note of the __Consumer key__ and the __Consumer secret__ displayed on this page and store this information somewhere safe, as you will need it later. At the bottom of the page under __Token Headings__ click the button labeled __Create my access token__. This will generate your application’s __Access token__ and it’s __Access token secret__, which allow your application to make Twitter API calls. If they are not displayed immediately, refresh your browser until they appear. Write them down and store them in a safe place for later.

## Setting up Your Dev Environment

You are almost ready to start tweeting. Before we can do that, however, we just have to make sure a few tools are in place that will allow our code to work. Use `pip` to download the following packages:

* PbPython
* Tweepy

PbPython is the Pandorabots Python SDK that allows us to interact with the Pandorabots API, and Tweepy is a Python library that allows us to do the same with Twitter. Once these are installed, we are ready to run our python program.

## Final Steps

Now you are ready to start tweeting! Download [twitter\_bot.py](https://github.com/pandorabots/twitter_bot.py/blob/master/twitter_bot.py), and insert your __Pandorabots user key, Consumer key, Consumer key secret, Access token, and Access token secret__ where indicated. You will also have to provide your __bot's name, your appname, and the server it is hosted on__. Here is the part of twitter_bot.py where you put in your credentials:

    import tweepy
	  import re
	  import os.path
	  import time
	import argparse
	import sys
	from pb_py import main as pandorabots_api

	host = 'INSERT HOST SERVER HERE'
	botname = 'INSERT BOT NAME HERE'
	app_id = 'INSERT APPNAME HERE'
	user_key = 'INSERT USER KEY HERE'

	access_token = 'INSERT ACCESS TOKEN HERE'
	access_token_secret = 'INSERT ACCESS TOKEN SECRET HERE'

	consumer_key = 'INSERT CONSUMER KEY HERE'
	consumer_secret = 'INSERT CONSUMER SECRET HERE'

To test your program, log onto your twitter account and tweet at your bot “Hey there @your\_bots\_twitter\_name”. Then run the Python program from the command line via the command `python twitter_bot.py` and see your bot tweet back! To run the program continuously, constantly monitoring for and responding to new tweets, run `python twitter_bot.py --continuous true`.

######Next Steps

Congratulations! You have created a basic program that tweets back at users using your bot's brain. However, this is just the beginning of what you can do. You could make your bot tweet at twitter users whose tweets contain certain keywords, or make your bot comment on whatever current events are trending. The possibilities are endless! We encourage you to modify this code and come up with new and exciting ways to use your Pandorabot on Twitter. Happy coding!

_If you have any questions or concerns please contact info@pandorabots.com. It should be noted that this code is intended for personality-driven bots, and that Twitter has no official policy on bots. Use this code with caution and do not abuse the Twitter platform. For more information on this, please take a look at Twitter’s [Developer Rules of the Road](https://dev.twitter.com/terms/api-terms). Enjoy!_
