---
layout: aiml
title: thatstar
---

### &lt;thatstar /&gt;

The *thatstar element* is used to echo wildcard contents found inside of `<that>` tags.

#### Attributes

`index`
Specifies the index of the wildcard to echo. If no index is specified, defaults to 0.

#### Usage


    <category>
    <pattern>I LIKE IT TOO</pattern>
    <that>I LIKE *</that>
    <template>What do you like best about <thatstar /></template>
    </category>

>**Input:** ...  
**Output:** I like coffee.  
**Input:** I like it too.  
**Output:** What do you like best about coffee?

This type of category is useful for dealing with pronoun resolution (*anaphora*). If the user inputs the word "it", you can implement a that element and a thatstar element to keep a reference to the original noun in question.
