---
layout: aiml
title: request
---

### &lt;request /&gt;

The *request element* returns the user's input specified by its historical index value.

#### Attributes

`index`
Specifies the historical index of the user's input to recall. `index="0"` refers to the current input.

#### Usage

    <category>
    <pattern>WHAT DID I JUST SAY</pattern>
    <template><request index="1" /></template>
    </category>

>**Input:** Hi  
**Output:** Hi there!  
**Input:** What did I just say?  
**Output:** Hi
