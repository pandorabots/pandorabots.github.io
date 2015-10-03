---
layout: aiml
title: rest
---

### &lt;rest&gt;

The *rest element* is a list processing tag that returns the contents of the element while omitting the first word.

#### Usage

    <category>
    <pattern>REST *</pattern>
    <template><rest><star /></rest></template>
    </category>

>**Input:** Rest A B C D  
**Output:** B C D
