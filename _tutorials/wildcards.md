
# Wildcards in AIML

The Ultimate Default Category (UDC) is used by the bot to provide an answer if no other suitable category can be matched.

    <category>
    <pattern>*</pattern>
    <template>I have no answer for that.</template>
    </category>
    
We use an asterisk `*` in the pattern to capture the user's input. This symbol in AIML is known as a wildcard.

Wildcards are used to capture many inputs using only a single category. 
There are a number of different wildcards that can be used in AIML.

## The * Wildcard

The `*` symbol is able to capture one (1) or more words in the user input

    <pattern>HELLO *</pattern>
    
This pattern would match all of the following inputs:

Hello there!  
Hello Daniel.  
Hello my good friend.  
Hello, anyone there?  

But **not** the word "Hello" by itself, bacuase there must be at least one word captured by the `*` wildcard to form a match.

## The ^ Wildcard

The `^` symbol is also a wildcard, however, it can capture 0 or more words.

    <pattern>HELLO ^</pattern>
    
This pattern would match all of the following inputs:

Hello.  
Hello there!  
Hello Daniel.  
Hello my good friend.  
Hello, anyone there?  

What if both patterns exist? Which one will form a match? 

#### HELLO *
#### HELLO ^

Wildcards are ranked in order of priority, so that certain patterns will take precedence over others.

The `^` has higher priority, so if the input is "Hello there", the 2nd pattern would be matched.

## Exact Matches

If a pattern forms an exact match with the input, that category will take precendence 
over any containing the `^` or `*` wildcards that it could potentially match.

#### HELLO THERE  
#### HELLO ^
#### HELLO *  

If the input is "Hello there", the first pattern will match before the other wildcard patterns.

## The _ and # Wildcards

There are two other wildcards, `_` and `#`. These wildcards take the highest priority 
when matching. Even if the input forms an exact match with a pattern, the match can be 
overridden by a pattern containing one of these wildcards.

#### HELLO _  
#### HELLO THERE  

If the input is "Hello there", the first pattern will form a match.

`_` is a "1 or more" wildcard (like `*`)  
`#` is a "0 or more" wildcard (like `^`)

Be very careful when using these wildcards because they will override all other patterns, including exact match!

## Matching Priorities

This example shows the matching priority for all four wildcards, along with a pattern that contains an exact match.

### HELLO # > HELLO _ **>** HELLO THERE **>** HELLO ^ **>** HELLO *  

## Highest Priority Matching

Sometimes there is an exact match that we would like to take highest priority, overriding the `_` and `#` wildcards.
We can use the $ sign to signify that a pattern will be matched first given a particular word.

    <pattern>$WHO IS MIKE</pattern>
    :
    <pattern>_ MIKE</pattern>
    
The first pattern matches "Who is Mike?" while the second pattern matches all other inputs ending with "Mike".

Note, that the $ symbol is not a wildcard. It is a marker that says "for this particular word(s) 
(e.g WHO), override the category that would have otherwise been matched.

## Visualizing Matching Priority

All of the bot's AIML categories are loaded into a structure called the "Graphmaster." The order in which
patterns take matching priority can be visualized in the Graphmaster, such as this internal representation:

## Multiple Wildcards

You can have more than one wildcard per pattern. You can echo multiple wildcards in your 
pattern by using `<star index="x" />`, where x corresponds to the index number (position in 
the sentence) of the wildcard. Not including the index assumes the first wildcard. For example:

    <category>
    <pattern>MY NAME IS * AND I AM * YEARS OLD</pattern>
    <template>Hi <star/>. I am also <star index="2" /> years old!</template>
    </category>
    


