---
layout: aiml
title: map
---

### &lt;map&gt;

The *map element* is used to reference a `.map` file, which attempts to match the map element's contents to one of its own properties, returning the property's value. Maps are data structures that provide key-value pairs.

#### Attributes

`name` (required)  
Specifies the name of the `.map` file to match contents against.

#### Usage

This example uses [state2capital.map](https://github.com/pandorabots/rosie/blob/master/lib/maps/state2capital.map) and [state.set](https://github.com/pandorabots/rosie/blob/master/lib/sets/state.set), both from the Rosie chatbot repository.

    <category>
    <pattern>WHAT IS THE CAPITAL OF <set>state</set></pattern>
    <template>
      <map name="state2capital"><star /></map> is the capital of <star />
    </template>
    </category>

>**Input:** What is the capital of California?  
**Output:** Sacramento is the capital of California

This category shows how maps and sets can be used in conjunction with each other to create "facts" in your bot's knowledge base. The `state.set` file is called in the pattern to verify that the user's input actually contained a state. If the wildcard contents does exist in the set file, it is then passed in as an input to `state2capital.map`. If it matches any of the keys in the map file, then the map element will return as associated value.
