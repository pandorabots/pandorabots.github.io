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
    <template><srai>HI</srai></template>
    </category>
    
    <category>
    <pattern>BONJOUR</pattern>
    <template><srai>HI</srai></template>
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


Another use case of the srai element is to provide a recursive response, to build a more complex response based on elements within the user's input.  For example, you have a bot named "Buddy":

User: You can say that again Buddy!  
Bot: Once more? "that".  

Your bot may not have a specific response to the pattern "YOU CAN SAY THAT AGAIN BUDDY". Instead you can build a response to the user input from partial phrase categories:


In step 1, the patterns with "_" match first based on AIML 2.0 wildcard priorities (from highest to lowest), for example:  
`# AGAIN > _ AGAIN > THAT  AGAIN >  ^ AGAIN > * AGAIN`

Whatever matches either wild-card symbol becomes the value of <star/>.


<table class="table table-striped table-bordered table-condensed">
    <tr><th>Step</th><th>Normalized Input</th><th>Matching Pattern</th><th>Template</th><th>Response</th></tr>
    <tr><td>1</td><td>YOU CAN SAY THAT AGAIN BUDDY</td><td>_ &lt;bot name="name" /&gt;</td><td>&lt;sr /&gt;</td><td></td></tr>
    <tr><td>2</td><td>YOU CAN SAY THAT AGAIN</td><td>_ AGAIN</td><td>Once more? &lt;sr /&gt;</td><td>Once more?</td></tr>
    <tr><td>3</td><td>YOU CAN SAY THAT</td><td>YOU CAN *</td><td>&lt;sr /&gt;</td><td>Once more?</td></tr>
    <tr><td>4</td><td>SAY THAT</td><td>SAY *</td><td>"&lt;person /&gt;".</td><td>Once more? "that".</td></tr>
</table>

Steps 1 through 3 illustrate the common AIML templates that use the abbreviated ` <sr/>` tag. Remember, &lt;sr/&gt; = &lt;srai&gt;&lt;star/&gt;&lt;/srai&gt; See [AIML Reference](http://docs.pandorabots.com/aiml/sr/) for details.

The categories with the patterns "_ &lt;bot name="name" /&gt;" and "YOU CAN *" simply reduce the sentence to whatever matches the wildcard, as illustrated by steps 1 and 3.

Combining the `<sr/>` with an ordinary text response, as step 2 with the pattern "_ AGAIN". The phrase "Once more?" becomes part of any reply ending in "AGAIN".

The category in step 4 with "SAY *" is a default that often produces logically correct but amusing dialogue:

User: Say Hello in Swedish.  
Bot: "Hello in Swedish."  

or as in this case:

User: Say that.  
Bot: "that."  

Using the `<person/>` tag in this examples allows for the transforming of any pronouns. (See [AIML reference](http://docs.pandorabots.com/aiml/person/) for more details).

User: Say you are a fish again.  
Bot: Once more?  "I am a fish".  

In this particular case, you might not want pronoun transformation; it's just included as an example for illustration.

Why reduce a complex sentence structure to simpler forms? These 4 categories can respond to a large number of inputs, not just the example, and can make a bot's response seem more human-like.
