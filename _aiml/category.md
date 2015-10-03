---
layout: aiml
title: category
---

### &lt;category&gt;

The *category element* delimits a base unit of knowledge in an AIML-based chatbot. In a very broad sense, a single category accepts an input, and returns an output.

All AIML elements (with the exception of the AIML root element and the topic element) must be contained within a category block.

#### Usage

    <category>
    <pattern>HI</pattern>
    <template>Hello world!</template>
    </category>
