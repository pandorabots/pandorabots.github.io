---
layout: aiml
title: sraix
---

### &lt;sraix &gt;

The *sraix element* allows a bot to call categories that exist within another bot, and return response as if it was its own. This allows the creation of many bots, each with a specific purpose, that may connect with each other to form a sort of bot network.

#### Attributes

`bot` (required)
Specifies the bot to call out to, defined by the `botid`. On the Pandorabots Playground, the `botid` is equivalent to `username/botname`. On the Developer Portal, it is defined as `app_id/botname`.

#### Usage

Imagine a user named "djf" with two bots, "olimpia" and "alice". You could forward inputs from olimpia to alice, and return alice's response to the user conversing with olimpia:

    <!-- from bot djf/olimpia -->
    <category>
      <pattern>WHAT IS FOO</pattern>
      <template><sraix bot="djf/alice"><input/></sraix></template>
    </category>

    <!-- from bot djf/alice -->
    <category>
      <pattern>WHAT IS FOO</pattern>
      <template>Foo is bar.</template>
    </category>

So when talking to djf/olimpia, the following is possible:

>**Input:** What is foo?  
**Output:** Foo is bar.  
