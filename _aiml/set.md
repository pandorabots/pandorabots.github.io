---
layout: aiml
title: set
---

### &lt;set&gt;
The *set element* is used differently depending upon if it is in the pattern or the template.

### SET USED IN PATTERN

In a category's pattern, the *set element* is used to access values in a bot's set file, which is a list of unique text strings. For example, a set file called "colors" might include a list such as:  
red  
orange  
yellow  
green  
blue  
indigo  
...

We can use sets to dramatically reduce our overall number of categories. Consider the following conversation:  
**Human:** Is green a color?  
**Bot:** Yes, green is a color.  
**Human:** Is blue a color?  
**Bot:** Yes, blue is a color.  
**Human:** is peanut butter a color?  
**Bot:** No, peanut butter is not a color.  
Imagine how many categories would be needed to cover every color in the spectrum!

Instead of giving each color its own category, we can create a set that contains all the colors, and write a single category that checks to see if the user's input contained one of those colors. This category will only be matched IF the user's input does, in fact, contain one of the colors in the set. Otherwise, the category will not be matched. The set functions like a wildcard. It captures one or more words found in the user's input.

#### Built-in Sets

Pandorabots have some build-in sets that are not visible in the list of bot files.

    <set>number</set>     -- matches any natural number
    
    
#### Usage
    <category>
    <pattern>IS <set>colors</set> A COLOR</pattern>
    <template>Yes, <star /> is a color.</template>
    </category>
    
    <category>
    <pattern>IS * A COLOR</pattern>
    <template>No, <star /> is not a color.</template>
    </category>
    
If the input contained a string not found in the set, then that pattern would not have formed a match. Because of this, we can provide a default answer using a * wildcard. The second category above matches if the input contains a string not found in the set.

**NOTE:** Sets take precedence over * and ^ wildcards, but can be overridden by _ # and an exact word match. The input captured by the `<set>` tags can be echoed using `<star/>`, just like a wildcard as shown in the usage example.  Set files are simple string array, such as:

    [["red"],["orange"],["yellow"],["green"],["blue"],["indigo"]]


### SET USED IN TEMPLATE 

In a category's template, the *set element* is used to set a predicate variable. Predicates are not hardcoded like properties, and can be initialized during a conversation. This means that input from the user can be echoed in the value of a predicate.

#### Attributes

`name` (required)
The name attribute specifies a name for the predicate you will set. The predicate can then be recalled under the same name using the get element. If you are setting a local variable rather than a predicate, use the `var` attribute instead.

#### Usage

    <category>
    <pattern>MY NAME IS *</pattern>
    <template>
      Nice to meet you, <set name="username"><star />.</set>
    </template>
    </category>
    
    <category>
    <pattern>WHAT IS MY NAME</pattern>
    <template>Your name is <get name="username" />.</template>
    </category>

**Input:** My name is Daniel.  
**Output:** Nice to meet you, Daniel.  
**Input:** What is my name?  
**Output:** Your name is Daniel.  

Note that there is no way to remove a predicate once it has been set to a value. You can overwrite it to a blank value such as:

    <set name="username"></set>
