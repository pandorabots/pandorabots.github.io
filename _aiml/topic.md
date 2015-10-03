---
layout: aiml
title: topic
---

### &lt;topic&gt;

The *topic element* allows your to contextualize categories according to the value of a predicate named is `"topic"`. Like the that element, topic binds a pattern to a particular context, however, it does this according to the persistance of a predicate rather than the previous bot response.

The topic element is unique to most AIML elements in that it appears outside of category blocks. You can wrap a number of categories within a topic element to bind all of those categories.

It should also be noted that the predicate name "topic" is reserved for this purpose.

#### Attributes

`name` (required)
Refers to a possible value of the topic predicate.

#### Usage

    <category>
    <pattern>LET US TALK ABOUT *</pattern>
    <template>
      OK, I like <set name="topic"><star /></set>
    </template>
    </category>
    
    <topic name="coffee">
    
    <category>
    <pattern>I DRINK IT PLAIN</pattern>
    <template>I prefer mine with cream and sugar</template>
    </category>
    
    </topic>

    <topic name="tea">

    <category>
    <pattern>I DRINK IT PLAIN</pattern>
    <template>I prefer mine with honey and lemon</template>
    </category>

    </topic>

>**Input:** Let us talk about coffee  
**Output:** OK, I like coffee  
**Input:** I drink it plain  
**Output:** I prefer mine with cream and sugar  
**Input:** Let us talk about tea  
**Output:** OK, I like tea  
**Input:** I drink it plain  
**Output:** I prefer mine with honey and lemon

This rudimentary example shows how setting the topic can also assist in contextualizing an input. If the user says something like "I drink it plain," the bot must have some way of knowing what "it" refers to in order to provide a relevent answer. This is illustrated in the above example via the different things one might add to coffee or tea. Depending on the value of the topic predicate, the bot will know which set of beverage additions to respond with.
