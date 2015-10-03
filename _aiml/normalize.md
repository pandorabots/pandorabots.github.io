---
layout: aiml
title: normalize
---

### &lt;normalize&gt;

The *normalize element* attempts to match the contents within the tags against the name of the properties found in ‘normal.substitution’.  If a match if found, the *normalize element* will replace the matching elements with the properties value.  

The properties found in the ‘normal.substitution’ file are used to modify every input that the bot may receive.

#### Usage

For when one is working with non-normalized information like information found in the *input element* as an example.  We can see this by trying to return this tag with and without the *normalize element*:

    <category>
    <pattern>THIS IS JOHN S</pattern>
    <template><input/></template>
    </category>

>**Input:** This is John’s.  
**Output:** This is John’s.

This output can be changed to be reflect a normalized input by using the normalize element. 

    <category>
    <pattern>THIS IS JOHN S</pattern>
    <template><normalize><input/></normalize></template>
    </category>

>**Input:** This is John’s.  
**Output:** This is John s

This can be helpful in scenarios where one is trying to train a bot with the *learn element*.

