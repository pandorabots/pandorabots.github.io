---
layout: aiml
title: pattern
---

### &lt;pattern&gt;

The *pattern element* is the block within each category that defines a linguistic pattern against which the user's input can be matched. The pattern may contain letters, numbers, spaces, and a number of other symbols including *wildcards*. 

The bot will search through all of its categories to form a match with the user input. 

#### Capitalization
AIML matching does not differentiate between capital and lowercase letters (i.e. if the client said either "hi" or "HI", the bot would match this category. Using all caps in the pattern is used to make the code more readable.

#### Normalization
Keep in mind, that the pre-processor strips the input of all punctuation, and other normalization substitutions. Therefore, as in the usage examples, do not include any periods, question marks etc. in the pattern tag. Also, you should include the normalized input, for instance "WHAT IS" rather than "WHAT'S".

#### Usage

    <category>
    <pattern>HI</pattern>
    <template>Hello there.</template>
    </category>
    
    <category>
    <pattern>WHAT IS YOUR NAME</pattern>
    <template>My name is Rosie</template>
    </category>
    

