---
layout: aiml
title: explode
---

### &lt;explode&gt;

The *explode element* is used to break a single word in to multiple words, by inserting spaces in between each character.

#### Usage

    <category>
    <pattern>EXPLODE *</pattern>
    <template><explode><star /></explode></template>
    </category>

>**Input:** Explode coffee  
**Output:** c o f f e e
