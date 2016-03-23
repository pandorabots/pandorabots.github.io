---
layout: default
title: Build a Concierge Bot
---

# Building a Concierge-style bot

The "Concierge" chatbot is actually a network of bots designed for the purpose of making recommendations about a service or product to the customer. We've built a music concierge that can recommend songs and artists to you based on your mood or current activity.

The network is made of up three distinct bot types, each of which takes on a different role:

- Personal
- Comparison engine
- Artist "expert"

We're going to take a look at how each of these bots work, as well as some of the AIML required for them to do so! Grab the code [here](https://github.com/pandorabots/concierge-network) to follow along.

The following AIML elements are featured heavily in this tutorial:

- [`<srai>`](/aiml/srai)
- [`<sraix>`](/aiml/sraix)
- [`<condition>`](/aiml/condition)
- [`<that>`](/aiml/that)
- [`<formal>`](/aiml/formal)

Make sure you are familiar with the high level concepts via the AIML Reference before you begin.

> **Note:** this music-oriented bot is just an example, but you can take these design patterns
with you when building your own Concierge-style bot.

## Architecture

![](/images/architecture.png)

The concierge bot network has a simple architecture that separates concerns by
dividing tasks between the bots. 

The *Personal bot* is the front-end for the network. This is the bot that your
users will be talking to, and has the responsibility of storing information that
your users share with it. This information can be reused later when making a
recommendation.

The *Comparison engine* is a bot that mimics a database which organizes musicians by genre. This allows the network to make a recommendation based on
the user's preference for a particular artist. We’ve given you a “pure AIML” solution in this example, but in reality you will probably want the power of a query language like SQL to fetch data from your database. It is not designed to be "talked"
to - rather, it can be used as a utility by the personal bot in an `<sraix>`
block.

Finally, the *Artist expert* is a bot that is knowledgeable about a particular
artist or musician. Again, this bot is not really designed to be talked to
directly - it is just a bot that can return information that the Personal bot
will share with the user.

## Comparison engine

Let's first take a look at the comparison engine so that we can have a little
context for how the personal bot is used. The comparison engine is a bot that
exposes two patterns to other bots. 

The first pattern is XSIMILAR *, which accepts the name of an artist in the
wildcard. It will return the name of another artist that makes music in the same
genre as the artist who was provided. For example:

{% highlight bash %}
Input: XSIMILAR Kendrick Lamar  
Output: Kanye West
{% endhighlight %}

> **Note:** the X prefix in some patterns is used to indicate that a pattern is intended to be a “private” category - in other words, these categories are used by the bot and it is not expected the user will ever type something like XSIMILAR. You may create your own private categories in this vein, and may use anything in the place of X (say, your initials), so long as the text is highly unlikely to appear in a user input.

The second pattern is XRANDOM * BLOCK ^, which accepts the name of a genre, and
returns a random artist from that genre. The BLOCK ^ portion is designed so that
you may optionally block an artist from being selected.

{% highlight bash %}
Input: XRANDOM hiphop BLOCK Tyga
Output: Iggy Azalea
{% endhighlight %}

You'll also notice the use of the `<set>` tags in the pattern of these
categories. Each set file (classical.set, edm.set, etc.) is just a grouping of
artists by genre. To add more artists to the comparison engine, just find the
correct set and add their name to the end!

This bot is really a "utility" - in other words, it’s not meant to be contacted
directly by your user. Instead, it is to be used via `<sraix>` in another bot.
Careful placement in the template of your calling bot can yield seamless
insertion of the output of the utility bot:

{% highlight html %}
<category>
  <pattern>I LIKE TO LISTEN TO DRAKE</pattern>
  <template>
    If you like Drake, you might also like <sraix bot="djf/musiccat">XSIMILAR DRAKE</sraix>
  </template>
</category>
{% endhighlight %}

## Artist expert

As an example of an "expert" bot, we've also included a bot that has some
information specific to an artist. Drakebot only has 2 categories:

{% highlight html %}
<category>
  <pattern>XBIO</pattern>
  <template>
    Aubrey Drake Graham (born October 24, 1986) is a Canadian rapper,
    singer, songwriter and actor. He was born in Toronto, Ontario. He first
    garnered recognition for his role as Jimmy Brooks on the television series
    Degrassi: The Next Generation. He later rose to prominence as a rapper,
    releasing several mixtapes before signing to Lil Wayne's Young Money
    Entertainment in June 2009.
  </template>
</category>

<category>
  <pattern>XRANDOMSONG</pattern>
  <template>
    <random>
      <li>0 To 100</li>
      <li>The Motto</li>
      <li>Marvin's Room</li>
      <li>Hold On, We're Going Home</li>
      <li>Worst Behavior</li>
      <li>6 God</li>
    </random>
  </template>
</category>
{% endhighlight %}

The first category is an example of how you might return some biographical information about the artist in question. The second category is an example of how you might store additional information about an artist like their playlist - here, the category is designed to return the name of a random song. You could build on this by including a link to the song on a streaming service, which might actually play the song when you click.

This bot is also a utility - rather than talking to it directly, we can use
`<sraix>` to call its private categories and insert its responses into another bot:

{% highlight html %}
<category>
  <pattern>TELL ME ABOUT DRAKE</pattern>
  <template><sraix bot="djf/drakebot">XBIO</sraix></template>
</category>
{% endhighlight %}

## Personal bot

Now that we've explained some of the bots in our network, let's take a look at
the centerpiece: the *Personal bot*. The personal bot is perhaps the most
important piece in the Concierge model - this bot is the user's gateway to using
other components like the comparison engine and the artist experts. The personal
bot has access to information about the user, and can make decisions based on
this information as to which bot may have a response to the user's input.

This bot also contains many *reductions*, which are categories that attempt to
"reduce" or parse what the user has said into something the bot might understand. 

{% highlight html %}
<category>
  <pattern>HELLO THERE</pattern>
<template><srai>HI</srai></template>
</category>
{% endhighlight %}

In this reduction, the pattern HELLO THERE does not return any text of its own, but instead uses `<srai>` to insert the return value of a different category (HI). We won't be sharing all of these in the tutorial because that would make it far too long, but you can check them out in the code on Github.

The personal bot is made up of a number of AIML files:

- activity.aiml - make recommendations based on what the user is doing
- artists.aiml - talk about musicians
- main.aiml - ultimate default category, prompts
- mood.aiml - make recommendations based on the user's mood
- recommend.aiml - make recommendations based on the user's favorite artist

### main.aiml

{% highlight html %}
<!-- UDC - catches inputs that don't match elsewhere -->
<category>
  <pattern>*</pattern>
  <template>I don't understand. Let's try something else. <srai>XPROMPT</srai></template>
</category>

<!-- HI - greetings redirect to XPROMPT -->
<category>
  <pattern>HI</pattern>
  <template>Hello there! <srai>XPROMPT</srai></template>
</category>

<!-- XPROMPT - prompts the user to give some information -->
<category>
  <pattern>XPROMPT</pattern>
  <template>
    <random>
      <li>How are you feeling?</li>
      <li>What are you up to right now?</li>
    </random>
  </template>
</category>
{% endhighlight %}

The goal of the Personal bot is to get some information from the user so that
it can make a recommendation about what they should listen to. You'll notice
that the first two categories both end with `<srai>XPROMPT</srai>`, which is a
design pattern we use to try and direct the conversation. You can use this all
over your AIML codebase to "tack on" the bot's question to the end of an output.

### recommend.aiml

The personal bot also features a file recommend.aiml, which makes a
recommendation to the user based on their favorite artist. 

{% highlight html %}
<category>
  <pattern>WHAT SHOULD I LISTEN TO</pattern>
  <template>
    <condition name="favoriteartist">
      <li value="unknown">Tell me one of your favorite artists.</li>
      <li><srai>XREC</srai></li>
    </condition>
  </template>
</category>
{% endhighlight %}

The bot relies on a predicate `favoriteartist` to make the recommendation. In
the first category, the `<condition>` block runs a check on the existence of
this predicate - if doesn't exist, the bot will ask the user for that info. If
it does exist, then the bot can move on the the `XREC` category to make the
recommendation.

{% highlight html %}
<category>
  <pattern>XREC</pattern>
  <template>
    If you like <formal><get name="favoriteartist"/></formal>, you might also like to listen to
    <sraix><bot><bot name="musiccat"/></bot>XSIMILAR <get name="favoriteartist"/></sraix>. 
    Want to hear a track?
  </template>
</category>
{% endhighlight %}

It is at this point that the personal bot reaches out to another bot in its
network. In this case, it is sending the user's `favoriteartist`
to the comparison engine bot, and inserting that bot's response into its own.
From the user's perspective, there is only one bot, but in reality the two
work together to form the network's response.

{% highlight bash %}
User: What should I listen to?
Bot: Tell me one of your favorite artists.
User: Ed Sheeran.
Bot: If you like Ed Sheeran, you might also Sam Smith. Want to hear a track?
{% endhighlight %}

### mood.aiml

The categories in this file are designed to give the user a recommendation based
on their current mood. 

{% highlight html %}
 <category>
  <pattern>HAPPY</pattern>
  <that>HOW ARE YOU FEELING</that>
  <template>Glad to hear it! You should listen to some <sraix bot="djf/musiccat">XRANDOM POP BLOCK</sraix> to complement your mood.</template>
</category>
{% endhighlight %}

All of these categories follow a similar model where the pattern is a different
mood, and the response calls out to the comparison engine bot to get a random
artist from a specific genre. If you remember our XPROMPT category, it will either return "What are you up to right now" or "How are you feeling?" - we use the `<that>` tag to ensure this
category will only match if the latter was the last response given by the bot.

## activity.aiml

This file is similar to the mood component, except it attempts to make a
recommendation based on the user's current activity. This could be working,
exercising, sleeping, etc. Depending on what the user is doing, the personal
bot will again reach out to the comparison engine to get a random artist from a
specified genre:

{% highlight html %}
<category>
  <pattern>WORKING</pattern>
  <that>WHAT ARE YOU UP TO RIGHT NOW</that>
  <template>I find <sraix bot="djf/musiccat">XRANDOM CLASSICAL BLOCK</sraix> to be great background music when I am working.</template>
</category>
{% endhighlight %}

## artists.aiml

The categories in this file are designed for interfacing with the artist expert.


{% highlight html %}
<category>
    <pattern>TELL ME ABOUT *</pattern>
    <template><srai>XBIO <star/></srai></template>
  </category>

<category>
  <pattern>XBIO *</pattern>
  <template>
    <think><set var="artist"><map name="artists"><star/></map></set></think>
    <condition var="artist">
      <li value="unknown">I don't know much about that artist.</li>
      <li><sraix><bot><bot name="app-id"/>/<map name="artists"><star/></map></bot>BIO</sraix> Want to hear a <star/> song?</li>
    </condition>
  </template>
</category>

<category>
  <pattern>YES</pattern>
  <that>WANT TO HEAR A * SONG</that>
  <template>
    <sraix><bot><bot name="app-id"/>/<map name="artists"><thatstar/></map></bot>REC</sraix> - <formal><thatstar/></formal>
  </template>
</category>
{% endhighlight %}

Take a close look at the `<think>` tag in XBIO *:

{% highlight html %}
<think><set var="artist"><map name="artists"><star/></map></set></think>
{% endhighlight %}

This block of AIML sets a local variable whose value comes from the artists.map
file, which is a sort of registry for all the artists expert bots in the network. This registry associates the artist’s name with the name of the artist expert bot.

{% highlight json %}
[
  ["Drake", "djf/drakebot"]
]
{% endhighlight %}

Right now we only have one expert bot in the network, but the idea is that the
bot might know about some artists, and might not know about others. In the case
that the bot does not have access to an expert bot, the first `<li>` will be
returned:

{% highlight bash %}
User: Tell me about Taylor Swift
Bot: I don't know much about that artist.
{% endhighlight %}

But if we have registered the artist bot in artists.map, then the second `<li>`
will be returned and the bot will contact the artist bot for an answer.

{% highlight bash %}
User: Tell me about Drake
Bot: Aubrey Drake Graham (born October 24, 1986) is a Canadian rapper ...
{% endhighlight %}

## Final notes

Hopefully you've already gotten your hands on the [code](https://github.com/pandorabots/concierge-network).
You can deploy this network yourself, just make sure to follow the directions in the Readme file
to properly route your `<sraix>` calls!







