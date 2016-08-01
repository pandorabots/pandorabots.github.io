---
layout: aiml
title: topic
---

### &lt;topic&gt;

The *topic element* allows you to contextualize categories according to the value of a built-in 
predicate named `"topic"`. Like the *that element*, topic binds a pattern to a particular context. 
This allows you to store a certain context for longer than just 1 interaction.

The *topic element* is unique to most AIML elements in that it appears outside of category blocks. 
You can wrap a number of categories within a *topic element* to bind all of those categories. 
These categories can only be matched if the topic has been set to a certain value. This can be 
used to write duplicate patterns whose templates vary depending on the context of the conversation

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

If you set a topic with no value, the value will be "unknown" based on bot property default-get.

    <set name="topic"></set>     --  topic = "unknown" 
    
Values for topic variables are only within the scope of an active conversation.
