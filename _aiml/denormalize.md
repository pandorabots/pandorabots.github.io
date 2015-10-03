---
layout: aiml
title: denormalize
---

### &lt;denormalize&gt;


The *denormalize element* attempts to match its contents against the names of properties found in `denormal.substitution`. If a match is found, the denormalize element and its contents will be replaced by the property's value.

The properties found in `denormal.substitution` are used to reverse transformations done by `normal.substitution`.

#### Usage

During input pre-processing, `normal.subsitution` removes punctuation. We can see this by echoing the part of the input that originally contained some puncutation:

    <category>
    <pattern>SAY *</pattern>
    <template><star /></template>
    </category>

>**Input:** Say pandorabots.com  
**Output:** pandorabots dot com

This punctuation can be re-inserted by using the denormalize element:

    <category>
    <pattern>SAY *</pattern>
    <template><denormalize><star /></denormalize></template>
    </category>

>**Input:** Say pandorabots.com  
**Output:** pandorabots.com
