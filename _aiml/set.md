---
layout: aiml
title: set
---

### &lt;set&gt;

The *set element* is used to set a predicate variable. Predicates are not hardcoded like properties, and can be initialized during conversation. This means that input from the user can be echoed in the value of a predicate.

#### Attributes

`name` (required)
The name attribute specifies a name for the predicate you will set. The predicate can then be recalled under the same name using the get element.

#### Usage

    <category>
    <pattern>MY NAME IS *</pattern>
    <template>
      Nice to meet you, <set name="username"><star />.</set>
    </template>
    </category>
    
    <category>
    <pattern>WHAT IS MY NAME</pattern>
    <template>Your name is <get name="username" />.</template>
    </category>

>**Input:** My name is Daniel.  
**Output:** Nice to meet you, Daniel.  
**Input:** What is my name?  
**Output:** Your name is Daniel.

