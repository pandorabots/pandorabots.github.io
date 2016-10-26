---
layout: default
title: Substitutions and sentence splitting
---

# Substitutions and sentence splitting

One new feature that was introduced in AIML 2.0 is the substitution file. These files are used to modify text strings being passed through your bot in such a way that both the AIML interpreter and your client can parse their meanings.

Substitution files look a lot like map files, but serve a different function. They look for defined sets of characters in text strings, and replace those sets of characters with new values. Depending on the substitution file, this transformation can either occur before the bot attempts to form a match with an input, or in the bot's response itself. Here's a basic example:

Input: I am waiting for you.  
Output: You are waiting for me.  

    <category>
    <pattern>I AM *</pattern>
    <template>You are <person><star/></person></template>
    </category>


The person tags found in the template denote that the bot should look for any words in the contained string that match one of the keys found in person.substitution. In this case, the contained string echoed by `<star/>` is "am waiting for you", and the word "you" can be found as a key in the person.substitution file. The bot will replace "you" with the value defined in the substitution file ("me"), and return the modified response.

Some of the substitutions that come preloaded with your bot have actually always been a part of the Pandorabots platform, however, it wasn’t until AIML 2.0 that we were able to offer the ability to actually customize them. Although some users will have no need to change the contents of these files, there may come time when you wish to add or remove options.

**person.substitution**

This file contains substitutions between first and second person pronouns. The above example transforms the second person pronoun "you" to the first person pronoun "me". This also works in reverse:

Input: You are waiting for me.  
Output: I am waiting for you.  

    <category>
    <pattern>YOU ARE *</pattern>
    <template>I am <person><star/></person></template>
    </category>

**person2.substitution**

This file is similar to person.substitution, but contains a few transformations between first and third person pronouns. These are rarely used in bots like Alice 2.0 and Rosie, but may come in handy.

Input: Give the password to me.  
Output: User has asked me to give the password to him or her.  

    <category>
    <pattern>GIVE THE * TO *</pattern>
    <template>User has asked me to give the <star/> to <person2><star index="2"/></person2></template>
    </category>

**gender.substitution**

Transforms gender pronouns to the opposite gender. Also rarely used, but potentially useful.

Input: Does it belong to him?
Bot: No, it belongs to her.

    <category>
    <pattern>DOES IT BELONG TO *</pattern>
    <template>No, it belongs to <gender><star/></gender></template>
    </category>

**normal.substitution**

The normal.substitution file functions a bit differently than the others, in that it can actually perform substitutions before the bot attempts to match the input to a pattern. This file is essentially a configuration file for the AIML preprocessor. Include this utility category in your bot:

Input: Say pandorabots.com.
Output: pandorabots dot com

    <category>
    <pattern>SAY *</pattern>
    <template><star/></template>
    </category>

This simple category allows us to see the AIML preprocessor at work. The normalize.substitution file defines the key ".com" with the value "dot com". By echoing the wildcard contents, we can see the "normalized" input string that matched the pattern. Try out some additional inputs to see other normalizations in action:

Input: Say I can’t hear you.  
Output: I can not hear you 

Input: Say isn’t.  
Output: is not  

Input: Say becasue.  
Output: because  

You can see that this file was also designed to normalize contractions, as well as some commonly mistyped words. Expanding this file will greatly increase your bot’s ability to understand inputs even when typos are present!

Note: The category described here is a very useful utility for debugging your bot! It’s a great tool to have available for use during development.

Please make sure you review the default normal.substitution file to see how inputs will be normalized. Some of the default normalization may not work for your use case, and you have the ability to customize the file as needed (removing substitutions, changing them or adding new ones).  

**denormal.substitution**

This file will "correct" normalizations done to your input, so that echoed inputs are returned with punctuation, etc. For example:

Input: Take me to pandorabots.com.
Template: Redirecting to pandorabots.com

    <category>
    <pattern>TAKE ME TO *</pattern>
    <template>Redirecting to <denormalize><star/></denormalize></template.
    </category>

Without the denormalize tag, `<star/>` would have returned "pandorabots dot com" as in the previous example. Instead, we are substituting the string "dot" with a period, as the input was originally typed.

**Sentence splitting**

Our AIML interpreter attempts to form a match with each sentence found in the input. Most of the time, an input will only be one sentence long, but in the case that it is longer, we divide the input based on a hardcoded list of "sentence splitters". These are punctuation marks that generally mark the end of a sentence.

We've recently changed our system to give more control to bot developers. This change is backward compatible, so your existing bots that do not have this new property will still work as normal. When you create a new bot, one of the default bot properties is called "sentence-splitters", and it includes the following items:

* **.** (period)
* **?** (question mark)
* **!** (exclamation mark)
* **。** (Japanese full stop)
* **？** (full width question mark)
* **！** (full width exclamation mark)

If you want to change your bot to support different sentence splitters, you will need to perform a couple changes to your bot files. For example, let’s say you want to define the semicolon as a sentence splitter:

Input: Hello; My name is Charles.  
Output: Hello. Nice to meet you, Charles.  

    <category>
    <pattern>Hello</pattern>
    <template>Hello.</template>
    </category>

    <category>
    <pattern>My name is *</pattern>
    <template>Nice to meet you, <set name="myname"><star/></set>.</template>
    </category>

First, update your bot property to add the semicolon to the "sentence-splitters" property
In the Playground Editor:

![]({{ site.baseurl }}/images/Screenshot-2014-10-14-at-5-27-26-PM-1.png)

Or, if you are updating the file in a text editor before uploading, add it to the JSON list item for "sentence-splitters".

    [["name", "testbot"],
    ["default-get", "unknown"],
    ["default-property", "unknown"],
    ["default-map", "unknown"],
    ["sentence-splitters", ".!?。？！;"],
    ["learn-filename", "pand_learn.aiml"],
    ["max-learn-file-size", "1000000"]]

You will also need to update normal.substitution to reflect this addition. By default, normal.substitution replaces the semicolon with a single space. This substitution pair needs to be deleted in order for the semicolon to be identified as a sentence delimiter in our system.

**Big Picture**

Substitutions are especially handy if you have connected your bot to messaging services or social media platforms (like [Twitter](http://blog.pandorabots.com/putting-your-pandorabot-on-twitter/)), where user inputs can often be colloquial or include things like emoticons, abbreviations, and hashtags. Luckily, using substitutions to transform inputs that include something like a #-->HASHTAG, you can code your bot to recognize all these things and more!
