---
layout: default
title: Browser Integration
---

# Browser Integration

Using the [pb-html package](https://github.com/pandorabots/pb-html), you can now easily deploy an application which provides a web interface for chatting with your chatbot.

If you're familiar with the now deprecated [AIML 1.0 system](http://www.pandorabots.com/botmaster/en/home), you'll probably remember how easy it was to publish your chatbot to a webpage using the "Custom HTML" tab in your dashboard. Now our APIs available via [chatbots.io](https://developer.pandorabots.com/) allow you integrate your chatbots into any application, however the "Custom HTML" feature was removed to protect the credentials and usage of your chatbot.

The [pb-html package](https://github.com/pandorabots/pb-html) is a simple web server that can be deployed to [Heroku](https://www.heroku.com/) with the click of a button. We've also provided a reusable, customizable chat interface for end-users to access and chat with your chatbot.

![](/images/pb-html.png)

## Setup

First, sign up for an account on [Heroku](https://www.heroku.com/). Then visit the [Github repository](https://github.com/pandorabots/pb-html) and click the "Deploy to Heroku" button. You'll be asked to provide your [Pandorabots API](https://developer.pandorabots.com/) credentials (it's assumed you already have a plan and have deployed a chatbot). Once you've clicked "Deploy for Free" and Heroku has built and launched your app, you may visit the site and start talking to your chatbot.

## End-user management

Our other integrations feature Redis as a way to manage your users over time. This works by mapping the user's phone number or username (depending on the platform) to a unique Pandorabots `client_name`, allowing the bot to remember information about the user in future messages and conversations.

With the browser, there is no phone number or username by which to identify the end-user. Instead, this implementation stores the `client_name` as a local variable, which is cleared when the user reloads the page. In other words, the chatbot will remember the user throughout the course of their conversation, but not after they have left the interface.

To mitigate this difference, you could store the `client_name` in a cookie so that it is saved even when the user leaves the page. A better option might be to implement some sort of authentication of your users, so that they can log in to a session that stores their client_name in memory. There is no "right" way to do this -- it all depends on the scope of your project!

## Development

If you'd like to customize your app, or make contributions to this project, first clone the repository. Once inside, run `npm start` to launch the app. You can then run `npm run watch` in a new terminal window to automatically build your frontend application when changes are saved.

This project uses [ReactJS](https://facebook.github.io/react/), a Javascript library made at Facebook for the purpose of building user interfaces.

### Styling

Some base styles are provided in src/public/css/base.css. There is also a file
src/public/css/style.css provided for you to do custom styling to the chat interface.
