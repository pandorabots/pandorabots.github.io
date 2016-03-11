---
layout: default
title: The Pandorabots CLI
---

# The Pandorabots CLI

While we already offer a number of tools for working with the Pandorabots API, we are proud to announce the newest member of our open-source arsenal: the [Pandorabots CLI](https://github.com/pandorabots/pb-cli). This tool is designed to let you manage and interact with your bots straight from the command line.

## Why is this great?

Of course, you could use an HTTP client like cURL to talk to the API. For example, to upload a file via cURL:

    $ curl -v -X PUT 'https://aiaas.pandorabots.com/bot/APP_ID/BOTNAME/file/example.aiml?user_key=USER_KEY'
      --data-binary @/home/mybot/example.aiml

That's a lineful! Wouldn't it be better if you could just freely type the commands, without worrying about all the necessary parameters to format a request?

This is exactly what we've done with the CLI:


    $ pb upload example.aiml


The CLI offers an easy and slick interface for doing all the things you'll need to create, update, and maintain your chatbots.

## Installation

The CLI itself is written in Javascript, so you'll need to setup node.js on your machine before you can install it. Luckily, node.js offers a number of [installers](http://nodejs.org/download/) for OS X and Windows users to make this very easy. You can also download binaries for Linux, or build yourself from the source code.

Node.js comes prepackaged with [npm](http://npmjs.org), which is a Javascript package manager that has an extremely vibrant community of modules and users. You can install the CLI using the `npm` command:

    $ npm install -g pb-cli

This will install the CLI globally to your machine, making the `pb` and `pandorabots` commands now available use in your command line.

## Configuration

The CLI introduces the concept of configuration files, which allow you to freely type commands as shown above. The configuration file is a JSON file called `chatbot.json`. It stores basic information about your application:

    {
      "app_id": "********",
      "user_key": "******",
      "botname": "*******"
    }

When you run a a CLI command, it will look in the current directory for the `chatbot.json` file. If it finds one, it will automatically add the necessary information to you call. You can create this file from scratch, or, run the `init` command to let the CLI build it for you. This command will prompt you for all the necessary information:

    $ pb init

## Usage

Once you have created a `chatbot.json` file, you can begin running all sorts of commands you might expect us to offer for the Pandorabots API:

    $ pb create
    $ pb upload example.aiml
    $ pb compile
    $ pb talk Hello world!

The CLI offers some additional tools not available through our REST API, such as the ability to upload multiple files at once:

    $ pb push

## Further information

Take a look at the CLI on [Github](https://github.com/pandorabots/pb-cli) for a complete list of the commands available. Please fork the project or report any issues or suggestions you may have!
