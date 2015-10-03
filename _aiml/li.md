---
layout: aiml
title: li
---

### &lt;li&gt;

The *list item element* can be a child of both `<condition>` and `<random>`. It allows you to attach mulitple responses, each of which is chosen under certain circumstances.

#### Attributes

`value` (optional)  
You may specify a value when the list item element is the child of a condition element. The list item element will be returned if the value matches that of the predicate referenced in the condition element.

#### Usage

Using `<li>` inside of a `<random>` element:

    <category>
      <pattern>HI</pattern>
      <template>
        <random>
          <li>Hello!</li>
          <li>Hola!</li>
          <li>Hallo!</li>
        </random>
      </template>
    </category>

Using `<li>` inside of a `<condition>` element:

    <category>
      <pattern>WHO AM I</pattern>      
      <template>
        <condition name="name">
          <li value="unknown">I don't know your name.</li>
          <li>Your name is <get name="name"/></li>
        </condition>
      </template>
    </category>
