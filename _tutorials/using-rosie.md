---
layout: tutorials
title: Using Rosie
---

# Using Rosie

***Update:*** *We will occasionally push changes to the Rosie repository to improve the existing content. We highly suggest that you watch the project on [Github](https://github.com/pandorabots/rosie) to keep track of future updates.*

*Unless otherwise noted, future updates to Rosie will be placed in **z_update.aiml**. If you are already working with a version of Rosie, you should upload only this file to your bot. This will allow you to get the updates without overwriting files you may have done custom work on.*

Original platform users may be wondering where they can access pre-written AIML (like Dr. Wallace’s ALICE bot) to use as base content for their bot. We provide such open-source AIML content to save users the hassle of “reinventing the wheel”  by recreating basic functionality.

Enter [Rosie](https://github.com/pandorabots/rosie): she’s free to download, a fork of the ALICE 2.0 project, and optimized for use on the Pandorabots 2.0 platform. This post will show you how to start building a custom chatbot on top of the Rosie “brain.”

Before beginning, be sure to read the [Build a Bot Tutorial](https://playground.pandorabots.com/en/tutorial/) on the Pandorabots [Playground](https://playground.pandorabots.com/en/).

Here are the different files you’ll find in Rosie:

## Properties (rosie.properties)

A property is a variable that is global to all users of a bot. Generally, properties are used to store information about your bot: it’s name, age, status, etc. Rosie comes with an extensive properties file that you can edit to easily customize your bot’s personality. This is a great place to get started exploring Rosie’s capabilities. Try giving the pre-existing properties some custom values, or add new properties as you see fit.

## Bot information (bot_profile.aiml, personality.aiml)

These two files contain categories that actually implement the variables you have defined in the properties file. For example, Rosie comes preloaded with a property named “job”, and the property is integrated in a category found in bot_profile.aiml:

    <category><pattern>JOB</pattern>
    <template>I am a full-time <bot name="job"/>.</template>
    </category>

Now, when the JOB pattern is matched, the category will give a response that contains whatever value you have assigned the “job” property in the rosie.properties file.

Most of the fun in bot development is not only picking out custom property values for your bot, but also customizing the templates in which these values are returned. For example, I might edit the above category to add a little more flair to my bot:

    <category><pattern>JOB</pattern>
    <template>By day, I am a <bot name="job"/>. At night, I crawl the internet looking for pictures of cats wearing funny hats.</template>
    </category>

## Client information (client_profile.aiml)

Pandorabots are amazing because of their uncanny ability to remember personal information about the people talking to them. These pieces of information are stored as predicate variables, which are local to the particular client. The client_profile.aiml file contains mostly categories designed to both set and recall these predicates in the course of conversation:

    <category><pattern>I AM FROM *</pattern>
    <template>Is that where you live now?  <think><set name="birthplace"><star/></set></think></template>
    </category>
    <category><pattern>MY BIRTHPLACE</pattern>
    <template><get name="birthplace"/></template>
    </category>

This is another great file to customize, by changing the existing templates, or by adding new categories that set new predicates about your user.

## Contextual categories (udc.aiml, that.aiml, train.aiml)

The ultimate default category (UDC) is designed to give a response when your bot was unable to match the user’s input with any other category. If your bot is in its beginning stages of development, the UDC will be an indispensable tool.

    <category><pattern>*</pattern>
    <template>I didn’t understand that!</template>
    </category>

You can customize this file by changing the default list elements in the UDC template, or by adding your own additional list elements.

The that.aiml file is included mostly as an example of what can be done with context in AIML using the `<that>` tag. The `<that>` tag is used to attach a category to the previous answer given by a bot; in other words, a category with a `<that>` tag can only be matched if the the previous response matches the contents of `<that>`. For example:

    <category><pattern>YES</pattern>
    <that>IS IT A NICE PLACE</that>
    <template>What do you like best about it?</template>
    </category>

Out of context, the input “yes” could be referring to anything. This category’s `<that>` tag, however, places the yes in the context of the bot’s previous response (IT IS A NICE PLACE).

The that.aiml file included contains a number of these useful context categories. Feel free to delete, edit, or add more context categories!

Finally, the train.aiml file is designed for you to easily take advantage of the AIML 2.0 `<learn>` tag, which allows a client to generate a new category during conversation.

## Environment configuration (config.aiml, rosie.pdefaults)

The configuration file is designed with the application developer in mind. It allows you to set a predicate based on the environment to which the bot is being talked to (browser, mobile, screenless, etc.).

Think about it this way: let’s say I have a category that displays a picture of a cat when activated. What if there is no screen interface for my bot? You can use the “env” predicate in categories whose response depends on the condition of the client’s environment. Here’s an example from bot_profile.aiml:

    <category><pattern>PIC</pattern>
    <template>
    <condition name="env">
    <li value="browser">My picture: <bot name="picture"/></li>
    <li>You'll have to connect me to a browser if you want to see a picture.</li>
    </condition>
    </template>
    </category>

The default value of the “env” predicate is “browser”. If the value of “env” is browser, the bot will respond with the first list item. If the “env” predicate is set to anything else, the second list item will serve as the response.

You can use the categories found in config.aiml to set these types of predicates. You can then write AIML categories whose response is dependent on the value of these predicates:

    <category><pattern>XSET ENV *</pattern>
    <template>Environment is <set name="env"><star/></set></template>
    </category>


## Utilities (date.aiml, dialog.aiml, roman.aiml, utilities.aiml)

These files are all tools and utilities that allow your bot to perform various functions. The date.aiml file, for example, allows you to type SEASON and receive the current season (based on the current date).

The AIML found is these files is very useful for any bot developer. You shouldn’t have to modify these files, but if you do, you’ll probably want to avoid changing anything other than template-side contents.

## Filters (inappropriate.aiml, insults.aiml, profanity.aiml)

These files act as filters when someone talking to the bot is attempting to say something “naughty.” Depending on what type of bot you are building, you may or may not want to include these files. They are quite comprehensive, so we included them in Rosie’s core.

Rosie’s UDC contains a randomized list of responses. Robust chatbots will often have hundreds of potential responses in this list. Rosie’s UDC has about 50 different responses; you may edit these and add to the list as you see fit.

## Reductions (reductions1.aiml, reductions2.aiml, reductions_update.aiml)

Try asking Rosie about her job:

What is your job? I am a full-time chatbot.
Do you have a job? I am a full-time chatbot.

The reason these inputs are able to match our JOB category is because Rosie is chalk-full of useful reduction categories that simplify common inputs into succinct denominations. In other words, Rosie will automatically translate DO YOU HAVE A JOB and WHAT IS YOUR JOB to the much simpler JOB. By modifying the template of the single JOB category, we can effectively modify the answer given to a large number of inputs.

The bulk of Rosie (and ALICE) is made up of these reduction categories. For example, here are some categories from reductions1.aiml:

    <category><pattern>WHAT COUNTRY AM I *</pattern>
    <template><srai>MY COUNTRY </srai></template>
    </category>
    <category><pattern>WHAT COUNTRY ARE WE *</pattern>
    <template><srai>MY COUNTRY </srai></template>
    </category>
    <category><pattern>WHAT COUNTRY ARE WE IN</pattern>
    <template><srai>MY COUNTRY </srai></template>
    </category>
    <category><pattern>WHAT COUNTRY IS THIS</pattern>
    <template><srai>MY COUNTRY </srai></template>
    </category>

These categories reduce similar inputs to the simple pattern MY COUNTRY. You can modify the bot’s response to all four of these patterns by finding the MY COUNTRY category and changing the contents of its template.

Although the reductions files are at the heart of Rosie’s prowess with natural language understanding, you will most likely not have to edit anything in these files. However, it would be beneficial to skim through to get a feel for the types of reductions that are implemented in Rosie.

## Sets and Maps

Finally, Rosie contains a large number of set and map files that were inherited from ALICE 2.0. Some of these are implemented in the AIML, others are not; but because they are such valuable resources for pattern matching and storing key-value pairs, they are included.

## Substitutions

Rosie comes preloaded with all the same substitution files found when you create a new bot on the [Playground](https://playground.pandorabots.com/en/).

Start using Rosie now by downloading the [github files](https://github.com/pandorabots/rosie) and uploading them to a bot on the [Playground IDE](https://playground.pandorabots.com/en/).
