---
layout: aiml
title: srai
---

### &lt;srai&gt;

The *srai element* allows your bot to recursively call categories after transforming the user's input. The acronym "srai" has no official meaning, but is sometimes defined as *symbolic reduction* or *symbolic recursion*.

#### Usage

The most typical use case of the srai element is to "reduce" an input by removing unecessary words, or by translating the input in to a shorter, more concise version.


    <category>
    <pattern>HELLO GOOD DAY</pattern>
    <template><srai>HI</template>
    </category>
    
    <category>
    <pattern>BONJOUR</pattern>
    <template><srai>HI</template>
    </category>
    
    <category>
    <pattern>GUTEN TAG</pattern>
    <template><srai>HI</srai></template>
    </category>
    
    <category>
    <pattern>HI</pattern>
    <template>Hello there!</template>
    </category>             

In the case that the user's input is "Hello good day," "Bonjour," or "Guten Tag," the first three categories will recurse, and give the bot a new input "HI". This will then match the fourth category, returning its response to the user.