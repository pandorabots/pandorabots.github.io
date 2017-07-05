---
layout: default
title: Simple FAQ Chatbot
---


# Developing a simple FAQ chatbot in AIML

A Frequently Asked Questions (FAQ) chatbot connected to a messaging platform or to your website, is a great use case for a Pandorabot. We've come up with an approach to build a quick FAQ chatbot. The purpose of this article is to step you through the thought process of this approach for a limited set of FAQs.

This process assumes you understand basic AIML terminology such as [categories](http://pandorabots.github.io/aiml/category/), [symbolic reductions](http://pandorabots.github.io/aiml/srai/) and [wildcards](http://docs.pandorabots.com/tutorials/wildcards/).

## Step 1: Gather your list of questions and answers

If you have chat or inquiry history with your customers, you might have a list of frequently asked questions, as well as the most common ways your customer asks a question that results in the same answer.  For example, these questions may all result in the same answer as shown below:

* How do I sign up?
* How do I sign up for your services?
* I want to sign up now
* Where do I signup?
* Where do I sign up for your service?
* I don't know how to sign up
* I'm having problems signing up

Example answer:
* Go to fabcompany.com/services and click the SIGN UP button in the middle of the page.

Make sure that all the questions you've listed actually map to the same answer. For instance, you might want to provide a different answer to "I'm having problems signing up", such as "Please contact our support staff at XXX-XXX-XXXX". 


*Note*: using a chatbot to solicit more information from your customer to identify a problem is a different chatbot use case. These approaches can be combined into a single Pandorabots though!


## Step 2: Develop Canonical Forms

In the example above, you have one answer and at least 6 different ways to ask the same basic question about "sign up". We call the base input, the canonical form (also known as "intents"). 

You can pick one question as your canonical form, and build the base category:

    <category>
      <pattern>HOW DO I SIGN UP</pattern>
      <template>Go to fabcompany.com/services and click the SIGN UP button in the middle of the page.</template>
    </category>

Alternatively, we recommend using a naming convention with business name/department and type of question, such as FABSERVICESSIGNUP. 

    <category>
      <pattern>FABSERVICESSIGNUP</pattern>
      <template>Go to fabcompany.com/services and click the SIGN UP button in the middle of the page.</template>
    </category>


## Step 3: Develop Symbolic Reductions

There are several ways to develop Symbolic Reductions (the "many patterns, one reply" concept) as shown below. 

*Note on pattern and normalization*:  
Patterns must be stripped of punctuation and any other normalization that you have specified in your bot (i.e. normal.substitution file). For example, do not include "." (period) or "?" (question mark) and also if you have the substitution in your normal file, "don't" should be "DO NOT" in your pattern tags.

### Exact Match
If you have a list from chat history, you can just keep adding each question as a symbolic reduction (using [srai](http://pandorabots.github.io/aiml/srai/) AIML tag).

Example AIML would look like:

    <category>
      <pattern>HOW DO I SIGN UP FOR YOUR SERVICES</pattern>
      <template><srai>FABSERVICESSIGNUP</srai></template>
    </category>
    <category>
      <pattern>I WANT TO SIGN UP NOW</pattern>
      <template><srai>FABSERVICESSIGNUP</srai></template>
    </category>
    <category>
      <pattern>WHERE DO I SIGNUP</pattern>
      <template><srai>FABSERVICESSIGNUP</srai></template>
    </category>
         :
         :

This is simple but is not as flexible. This solution would not take into consideration typos or unconventional phrasing. 

### Wildcards & Keywords

Using [wildcards in AIML](http://docs.pandorabots.com/tutorials/wildcards/) pattern matching for your symbolic reductions can be more flexible. Start by identifying common words (i.e. keywords) in all your questions with the same answers. For example:

    <category>
      <pattern>_ SIGN UP _</pattern>
      <template><srai>FABSERVICESSIGNUP</srai></template>
    </category>

    <category>
      <pattern>_ SIGNUP _</pattern>
      <template><srai>FABSERVICESSIGNUP</srai></template>
    </category>

These reductions would apply to all 6 of the original questions.  You could even add reductions that addresses a very common misspelling of your keyword(s). For instance, the word "sign" is commonly misspelled as "sing" and "sigh"

    <category>
      <pattern>_ SING UP _</pattern>
      <template><srai>FABSERVICESSIGNUP</srai></template>
    </category>
    <category>
      <pattern>_ SIGH UP _</pattern>
      <template><srai>FABSERVICESSIGNUP</srai></template>
    </category>


The limitations of this approach is that it requires some human analysis, and too few words in the reduction can be less accurate. For instance, if someone inputs "I did sign up and hate it!", the chatbot's response would not work well if using the FABSERVICESIGNUP canonical form.

The great thing about AIML is that you can mix up these approaches building categories for your Pandorabot.

## Step 4: Putting it all together

Follow this process for each question and answer pair. For example, try these additional questions on your own.

* How do I get paid?
* How do I cancel your services?
* I need to speak to a real person.
* Who is your CEO?

Add all your categories to your Pandorabot, compile and start training your bot to see if you can break it!

## TIPS TO STREAMLINE THIS PROCESS

Using a spreadsheet to automate building categories with AIML tags can make this process easier.
![](/images/faqchatbottemplate.png)
