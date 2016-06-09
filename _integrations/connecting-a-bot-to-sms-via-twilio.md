---
layout: default
title: Twilio
---

# Connecting a Chatbot to Twilio

### *NOTE: Due to current changes in Twilio API this tutorial is obsolete, although some concepts may still apply.*

We've had a lot of interest recently from users wishing to connect their Pandorabot to messaging services like Twilio. In today's post, we'll take a look at how the Twilio platform works with apps, and how it can play with the Pandorabots API.

And thanks to Heroku's awesome [app.json Schema](https://devcenter.heroku.com/articles/app-json-schema), we've also made it ridiculously easy to get your SMS-enabled chatbot up and running.

This post assumes you've already got a [chatbots.io](https://developer.pandorabots.com/) account, and have created a bot that can be reached via the Pandorabots API. For more information, see  [Basic Bot Deployment](http://blog.pandorabots.com/basic-bot-deployment/) or [download the CLI](https://github.com/pandorabots/pb-cli) to get started.

## Setting up your Twilio app

[Twilio](https://www.twilio.com/) is a messaging and voice API that allows you to connect applications to a real phone number, and exchange data with that phone number via speech or text. To get started, you'll need an account and an SMS-enabled phone number (you should get one free number upon signing up).

Once you've completed the registration, click the "Show API Credentials" in the upper right corner of the page. Take note of the Authentication Token, as you'll need it to
validate requests from Twilio to your application.

> If you have signed up for the free plan on Twilio, make sure to read about [its limitations](https://www.twilio.com/help/faq/twilio-basics/how-does-twilios-free-trial-work) before continuing. At the time of this post, you have
to verify phone numbers individually before you can send SMS to your Twilio number.

## Deploy to Heroku

Twilio operates on a "webhook" model, which means that every time a text message is sent to your phone number, an HTTP request is sent to a URL of your choosing. Your application will live at this URL, and will take incoming messages from Twilio and pass them to the Pandorabots API for processing. When the API responds, your application can send a text message back to the sender by responding to the webhook's request.

![](/images/webhook.png)

We're going to use [Heroku](https://www.heroku.com/) to host our web app. Make sure you've signed up for an account (the free plan should be fine for this project). The code for your app is available in the main [Github repo](https://github.com/pandorabots/pandorabots-twilio-app). All you have to do is click the purple deploy button, enter in your API credentials and configuration, and Heroku will take care of building and launching everything for you.

## Configuring the webhook

You'll now need to return to Twilio to give it the URL of your application running on Heroku. Your URL is **http://your-app-name.herokuapp.com**, where App Name is the name that you chose when deploying the Heroku app (if you didn't choose one, scroll to the top of the deployment page to see the name Heroku automatically generated for you).

 Navigate to the "Phone Numbers" tab in your Twilio dash, and select your SMS-enabled
 number by clicking it on the left, and then clicking "Detailed View" in the modal
 that appears. Scroll to the "Messaging" section at the bottom of the page.

![](/images/messaging.png)

There are a few different ways to configure your messaging app on Twilio, but for this project we'll be using TwiML, a markup language devised by Twilio that helps you to create interactive voice and messaging appications.

Make sure you've selected "Configure with TwiML App," and select "Create a new TwiML App".

![](/images/create_twiml_app.png)

Give you TwiML App a name (this can be anything), and enter your Heroku URL in the "Request URL" field under "Messaging." Once you've saved and returned to the previous screen, make sure your TwiML app is selected to handle messaging for the phone number.

At this point, you should be able to send messages to your Pandorabot by texting the Twilio number. We've taken care of the implementation for you, including keeping track of your user's phone numbers so that the bot can remember information about them for later reference in conversation.
