---
layout: default
title: Using Data Dynamically
---

# Using Data Dynamically

Say you work in an industry like healthcare or financial services that typically deals with the treatment of “sensitive” end-user data. You want to build a conversational interface for your application, but you have concerns about using cloud services that might involve sending sensitive end-user inputs to third party services like Pandorabots for processing.

As a matter of policy, you may not send Pandorabots confidential information and, according to our [Terms of Service](https://developer.pandorabots.com/policies), you must ensure that you take proper steps to obtain rights to send any end-user data to our service. Fortunately, there’s a simple solution for platform users in sensitive verticals to avoid sending sensitive information to Pandorabots’ servers.

In the example below, we’ll explore how to use Pandorabots as the dialog engine for your application, without sending inputs containing personal health info (PHI) to your chatbot.

Let’s say you are building a senior care application designed to remind someone when to take their medicine. To build such an application, you may need confidential information about your end-users’ prescriptions (and permission from the end-user to access this data; if you’re unsure if you have permission or how to get it, you should seek legal advice).

You may think your chatbot needs “know” this information to have a meaningful conversation with a user about their medication, but actually, any sensitive data can be dynamically inserted into the bot’s response by your application after it has returned an answer. This allows you to use Pandorabots without exposing sensitive data to our system, which is not HIPAA compliant.

## Example
Mary Sue is using your application for the first time. When she logs in, your application will issue a call to Pandorabots that generates a *client_name* (see below) for Mary Sue so that the bot can maintain the state of her conversation.

When Mary Sue asks: “What medication do I need to take today?” your application will make a request to the bot on her behalf, sending the message with her pseudonymous unique identifier:

    {
      "question": "What medication do I need to take today?",
      "client_name": "aiaas-XXX-user-101"
    }

You can use Pandorabots to parse the meaning of the question, and return an appropriate answer. But because this question involves some PHI, let’s use Pandorabots to generate a template of what the answer will look like. Here, we’ll use the [mustache templating engine](http://mustache.github.io/):

    <category>
      <pattern>WHAT MEDICATION DO I NEED TO TAKE TODAY</pattern>
      <template>
        {% raw %}Here is your medication schedule: {{ user.schedule }}.{% endraw %}
      </template>
    </category>

Now, your application can look up Mary’s PHI in the database (indexed here by client_name), and render it in the bot’s response as needed:

    # pseudocode
    template = "Here is your medication schedule: {% raw %}{{ user.schedule }}{% endraw %}."
    user = database.getUser('aiaas-djf-user-101')
    response = mustache.render(template, user)

Here is the conversation from Mary’s perspective:

>**Mary:** What medication do I need to take today?  
**Bot:** Here is your medication schedule: 1 325mg aspirin daily.

As you can see, Pandorabots is occupying the role of a “dialog engine" that provides pre-formatted responses that your application can render. These templates can be used to render any sort of information that your application accesses.

Now, say Mary Sue has another, general question about Aspirin. This isn’t confidential information, and it’s fine to code that data directly into your bot’s knowledge base:

>**Mary Sue:** What is Aspirin?  
**Bot:** Aspirin: a synthetic compound used medicinally to relieve mild or chronic pain and to reduce fever and inflammation.

    <category>
      <pattern>WHAT IS ASPIRIN</pattern>
      <template>
        Aspirin: synthetic compound used medicinally to relieve mild or chronic pain and to reduce fever and inflammation.
      </template>
    </category>

If you have the information elsewhere, such as in a database or via a third-party API, you can use the same template technique as the PHI example to insert the proper information:

    <category>
      <pattern>WHAT IS ASPIRIN</pattern>
      <template>{% raw %}Aspirin: {{ drugs.aspirin }}{% endraw %}</template>
    </category>
