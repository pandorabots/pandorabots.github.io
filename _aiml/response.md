---
layout: aiml
title: response
---

### &lt;response /&gt;

The *response element* returns the bot's response specified by its historical index value.

#### Attributes

`index`
Specifies the historical index of the bot response to recall. `index="0"` refers to the current response.

#### Usage

    <category>
    <pattern>WHAT DID YOU JUST SAY</pattern>
    <template><response index="1" /></template>
    </category>

>**Input:** Hi  
**Output:** Hi there!  
**Input:** What did you just say?  
**Output:** Hi there!
