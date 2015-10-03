---
layout: integrations
title: Twilio
---

# Connecting a bot to SMS via Twilio

## Introduction

Suppose you've created a bot that you want to introduce to a larger audience. It could be a functional bot that answers questions about a product or service that your company offers, or a personality based bot that champions your brand. It could just be your own personal bot that tells jokes and funny stories, and you want your friends to be able to interact with it in a new and exciting way. Imagine that instead of having to download a new app, or go to a chat page on the internet, people could just send your bot a simple text message. Well, now they can, using Pandorabots and any third party messaging web service.

## Overview
This blog post demonstrates how to connect a Pandorabot to SMS using [Twilio](https://www.twilio.com/). Twilio is a cloud communications service which gives developers the ability to programmatically send and receive text messages and phone calls, among other things. By the end of this tutorial, you will have a simple app that will enable you to send and receive text messages from your Pandorabot. If you want an example, you can text Alice, the award-winning chatbot who inspired the movie *Her*, at this number: **1 724-359-4064**.

## First Steps

This tutorial assumes you have a bot deployed to our server. If you don’t have a bot yet, don’t worry, it’s easy to build one. Simply follow the instructions in our [Build a Bot Tutorial](https://playground.pandorabots.com/en/tutorial/) to get started. Also required is the `user_key ` found on your application’s page in the [Developer Portal](https://developer.pandorabots.com/). For more information on using the API, see our post on [Basic Bot Deployment](http://blog.pandorabots.com/basic-bot-deployment/).

The first step is creating an account with Twilio. A trial account is free and will be sufficient to complete this tutorial. Once you have your twilio phone number we can move on to setting up your development environment.

## Setting up your Local Dev Environment

We will be creating a Python web application using the [Flask](http://flask.pocoo.org/) microframework for Python, along with the [Pandorabots Python SDK](https://github.com/pandorabots/pb-python). You will need to have the following tools installed:

* Python
* Flask
* PbPython
* the twilio-python library

## Installing Python

Linux and Mac machines come pre-installed with Python. To see if you have Python, simply open a terminal on your computer and type:

    username% python

This should start the python interactive environment. If you do not have Python installed on your machine, follow the setup instructions on the [official Python page](https://docs.python.org/2/using/index.html).

## Installing Flask, PbPython, and twilio

Flask is a simple server written in Python. PbPython is the free Pandorabots SDK for Python. Twilio is the python helper library for the twilio api. We will install the three libraries using pip from the command line:

    username% pip install Flask
    username% pip install PbPython
    username% pip install twilio

For more information on installing pip, please see the documentation [here](https://pip.pypa.io/en/latest/installing.html).

## Creating your Flask App

Your flask application will be composed of one file. In your desired home folder, create a file named **run.py** and add the following code *(be sure to include your credentials where indicated)*:

    from flask import Flask, request, redirect
    import twilio.twiml
    from pb_py import main as api

    host = 'INSERT THE NAME OF THE SERVER YOUR BOT IS HOSTED ON HERE'
    user_key = 'YOUR PANDORABOTS USER_KEY'
    app_id = 'YOUR APPLICATION'S ID'
    botname = 'YOUR BOT'S NAME HERE'

    app = Flask(__name__)

    @app.route("/", methods=['GET','POST'])
    def bot_talk():
        """Respond to incoming texts with a text from your bot"""
        request_message = request.values.get('Body',  'twiliotest')
        bot_response = api.talk(user_key, app_id, host, botname, request_message)["response"]
        resp = twilio.twiml.Response()
        resp.message(bot_response)
        return str(resp)

    if __name__ == "__main__":
        app.run(debug=True)

Add the following category to your bot to test that your flask server is functioning correctly:

    <category>
	    <pattern>TWILIOTEST</pattern>
	    <template>Hello World!</template>
    </category>

Note: the pattern of our category corresponds to the string at the end of line 17 in **run.py**.

To test our flask server save **run.py**, and type at the command line:

    username$ python run.py
    * Running on http://127.0.0.1:5000/

Navigate to http://localhost:5000 in your browser. You should see your “Hello World!” message displayed.

## Connecting your server to the internet

Now that we have successfully created our flask server on our local machine, it’s time to deploy it to a public web address so that Twilio will be able to find it. Here are some tutorials that may help you with this task *(for the number above we used Heroku)*:

* [ngrok - Test your app without a web server](https://ngrok.com/)
* [Getting Started with Flask on Heroku](http://devcenter.heroku.com/articles/python)
* [How to deploy a Flask app on Webfaction](http://flask.pocoo.org/snippets/65/)
* [Deploying Flask on Apache, FastCGI, or uWSGI](http://flask.pocoo.org/docs/deploying/)
* [Deploying a Flask app on Dotcloud](http://flask.pocoo.org/snippets/48/)

Once you have your server deployed, the last step is to connect it to Twilio. Go to the [Numbers tab](https://www.twilio.com/user/account/phone-numbers/incoming) on your Twilio Account Page and click on your number. Add the public web address that you generated *(using one of the services listed above)* to the **Request URL** text box under the Messaging header. Save your settings and text your twilio number. Your bot will text back!

## Next Steps

You have just created a simple texting application for your bot. Congratulations! However, this app represents just the beginning of what you can accomplish. Using the Pandorabots and Twilio APIs one can do much more, such as respond to texts with images, or conduct persistent conversations with users all around the world. If you want to take your application to the next level, we recommend that you familiarize yourself with the documentation on [PbPython](https://github.com/pandorabots/pb-python) and [Twilio](https://www.twilio.com/docs). We are excited to see what you can create!
