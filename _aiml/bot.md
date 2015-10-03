---
layout: aiml
title: bot
---

### &lt;bot /&gt;

The *bot element* is used to recall custom bot properties defined in the `.properties` file. These variables are accessible to all users of the bot.

#### Attributes

`name` (required)  
Specifies the name of the property being recalled. If no property exists under the specified name, the bot element will return the value of the property named `default-property`.

#### Usage

    <category>
      <pattern>WHAT IS YOUR NAME</pattern>
      <template>My name is <bot name="name" /></template>
    </category>
