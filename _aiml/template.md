---
layout: aiml
title: template
---

### &lt;template&gt;

The *template element* is the portion of category that defines its return value. It can contain a variety of other elements: some which return text directly to the user, and some which cause recursion and trigger new categories. Every category must contain a template block.

#### Usage

    <category>
    <pattern>HI</pattern>
    <template>Hello there!</template>
    </category>
