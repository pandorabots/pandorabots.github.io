---
layout: default
title: Browser Integration
---

# Browser Integration

Using the pb-html package, you can now easily deploy an application which
provides an web interface for chatting with your bot.

If you're familiar with our old system, you'll probably remember how easy this
was to to using the "Custom HTML" tab in your dashboard. But with our release of
the new API, this feature was removed to protect the credentials and usage of
your bot.

The pb-html package is a simple web server that can be deployed to Heroku
with the click of a button. It comes with a slick little chat interface that
provides an easy way for users to access and chat with your bot.

## Setup

First, sign up for an account on Heroku. Then visit the [Github repository](https://github.com/pandorabots/pb-html)
and click the "Deploy to Heroku" button. You'll be asked to provide your
Pandorabots API credentials (it's assumed you already have a plan and have
deployed a bot). Once you've clicked "Deploy for Free" and Heroku has built
and launched your app, you may visit the site and start talking to your bot.

## User management

Our other integrations feature Redis as a way to manage your users over time.
This works by mapping the user's phone number or username (depending on the
platform) to a unique Pandorabots "client_name", allowing the bot to remember
information about the user in future messages and conversations.

With the browser, there is no phone number or username to identify the user by.
Instead, this implementation stores the client_name as a local variable, which
is cleared when the user reloads the page. In other words, the bot will remember
the user throughout the course of their conversation, but not after they have
left the interface.

To mitigate this difference, you could store the client_name in a cookie so that
the user's client_name is saved even when they leave the page. A better option
might be to implement some sort of authentication of your users, so that they
can log in to a session that stores their client_name in memory. There is no
"right" way to do this - it all depends on the scope of your project!

## Development

If you'd like to customize your app, or make contributions to this project,
first clone the repository. Once inside, run `npm start` to launch the app. You
can then run `npm watch` in a new terminal window to automatically build your
frontend application when changes are saved.

### Styling

Some base styles are provided in src/public/css/base.css. There is also a file
src/public/css/style.css provided for you to do custom styling!
