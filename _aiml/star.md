---
layout: aiml
title: star
---

### &lt;star /&gt;

The *star element* is used to echo portions of the user's input that were captured by wildcards.

#### Attributes

`index`
Specifies which wildcard to echo (used when multiple wildcard are present). If no index is specified, defaults to 0.

#### Usage

    <category>
    <pattern>MY FAVORITE * IS *</pattern>
    <template>Your favorite <star /> is <star index="2" /></template>
    </category>

>**Input:** My favorite color is blue  
**Output:** Your favorite color is blue
