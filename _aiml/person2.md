---
layout: aiml
title: person2
---

### &lt;person2&gt;

The *person2 element* is identical to the person element, however, it is used to transform pronouns between first and third person.

#### Usage

    <category>  
    <pattern>GIVE THE * TO *</pattern>  
    <template>User has asked me to give the <star/> to <person2><star index="2"/></person2></template>  
    </category>

>**Input:** Give the password to me  
**Output:** User has asked me to give the password to them
