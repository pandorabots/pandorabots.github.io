---
layout: aiml
title: random
---

### &lt;random&gt;

The *random element* can be used in conjunction with list item elements to provide a set of potential bot responses, one of which will be returned at random in the case that the category is matched.

This is a very useful tag to use in default categories, or categories that you think will be matched very often, because it can provide your bot with a less repetitive personality.

#### Usage

    <category>
    <pattern>HI</pattern>
    <template>
      <random>
        <li>Hello!</li>
        <li>Well hello there.</li>
        <li>Howdy.</li>
        <li>Good day.</li>
        <li>Hi, friend.</li>
      </random>
    </template>
    </category>

If the user's input is "HI", then one of the list item elements will be returned to the user at random.

