---
layout: aiml
title: get
---

### &lt;get /&gt;

The *get element* is used to return the value stored in a variable.

#### Attributes

You can use the `<get />` element to retrieve bot predicates and local variables.

`name`  
Specifies the name of the predicate to recall. If the predicate does not yet have a value, then the get element will return the default value for that predicate as specified in the `.pdefaults` file. If no default is specified, then the get element will return the value of the property `default-get`.

`var`  
Similar to the `name` attribute, but returns the value of a local variable.

#### Usage

    <category>
    <pattern>WHAT IS MY NAME</pattern>
    <template><get name="name" /></template>
    </category>

    <category>
    <pattern>MY NAME IS *</pattern>
    <template>Nice to meet you, <set name="name"><star /></template>
    </category>

>**Input:** What is my name?  
**Output:** unknown  
**Input:** My name is Daniel.  
**Output:** Nice to meet you, Daniel.  
**Input:** What is my name?  
**Output:** Daniel.

As seen in the above example, the first category returns the `default-get` property value ("unknown") in the case that no custom predicate `name` has been set. Once the second category has been engaged, the get element returns the custom value of the predicate.

To avoid returning the value of `default-get`, you can use a condition element to first check whether or not a predicate has been set. By using a wildcard as the list element's `value` attribute, we can check for any value of the predicate other than an empty string.

    <category>
    <pattern>WHAT IS MY NAME</pattern>
    <template>
      <condition name="name">
        <li value="*"><get name="name" /></li>
        <li>You have not told me your name.</li>
      </condition>
    </template>
    </category>
