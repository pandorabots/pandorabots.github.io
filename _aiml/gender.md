---
layout: aiml
title: gender
---

### &lt;gender&gt;

The *gender element* attempts to match its contents against the names of properties found in `gender.substitution`. If a match is found, the gender element and its contents will be replaced by the property's value.

The `gender.substitution` file contains properties whose names and values contain pronouns of opposite genders.

#### Usage

    <category>  
    <pattern>DOES IT BELONG TO *</pattern>  
    <template>No, it belongs to <gender><star/></gender></template>  
    </category>

>**Input:** Does it belong to her?  
**Output:** No, it belongs to him
