---
layout: aiml
title: topicstar
---
### &lt;topicstar&gt;

The *topicstar element* will either return the current topic if used outside of a *topic element* or the *wildcard element* when inside a *topic element*.  The *topicstar element* can also use index like the *star element* can, though this will return as the default case for empty predicates if no wildcards are present.

#### Usage

This is useful for knowing what your wildcards are actually containing or if you interested in what your topic is outside of your *topic element*. 

    <category>
    <pattern>I WOULD LIKE MILK</pattern>
    <template>Ok.<think><set name=”topic”>milk</set></think> You want <topicstar/></template>
    </category>

>**Input:** I would like milk.  
**Output:** Ok. You want MILK

As a reminder the topicstar element only takes what is inside the wildcard in the topic element’s name.

    <category>
    <pattern>I WOULD LIKE MILK</pattern>
    <template>Ok. <think><set name=”topic”>beverages milk</set></think></template>
    </category>
    
    <topic name=”beverages *”>
    <category>
    <pattern>WHAT DO I WANT</pattern>
    <template><topicstar/></template>
    </category>
    </topic>

>**Input:** I would like milk.  
**Output:** Ok.  
**Input:** What do I want?  
**Output:** MILK

