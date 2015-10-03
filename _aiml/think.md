---
layout: aiml
title: think
---

### &lt;think&gt;

The *think element* allows your bot to set predicates without actually displaying the contents of a set element to the user. This is sometimes referred to as "silently" setting a predicate.

#### Usage

Consider this example, which sets a predicate, but does so in a way that the contents of the set element is actually returned to the user as part of the template:

    <category>
    <pattern>MY NAME IS *</pattern>
    <template>
      Nice to meet you, <set name="name"><star /></set>
      </template>
      </category>

>**Input:** My name is Daniel  
**Output:** Nice to meet you, Daniel

You can use the think tag to set the `name` predicate, without actually repeating the value of the predicate to the user:

    <category>
    <pattern>MY NAME IS *</pattern>
    <template>
      <think><set name="name"><star /></set></think>
      I will remember your name.
    </template>
    </category>

>**Input:** My name is Daniel  
**Output:** I will remember your name
