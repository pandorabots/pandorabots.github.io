---
layout: aiml
title: person
---

### &lt;person&gt;

The *person element* attempts to match its contents against the `person.substitutions` file, which transforms pronouns between first and second person. If the contents forms a match with the name of a property in that file, then the person element and its contents will be replaced by the property's value.

#### Usage

    <category>
    <pattern>I AM *</pattern>  
    <template>You are <person><star/></person></template>  
    </category>

>**Input:** I am waiting for you  
**Output:** You are waiting for me

In the above example, the phrase "waiting for you" is echoed in the template using `<star />`. But because the tag descends from the person element, the pronoun "you" is transformed to "me".