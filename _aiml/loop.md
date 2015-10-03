---
layout: aiml
title: loop
---

### &lt;loop /&gt;

The *loop element* is used to iterate over a set of list item elements that are contained in a condition block.

#### Usage

To use the loop element, you must have a list item element with a value, and a second one that has no specified value. The loop element will be a child of the second list item, signifying that each time the second item is returned by the condition block, a loop occurs.

This means that you can modify a variable (like a predicate) when the second condition is met. If the value of the new predicate matches that of the first list item, then the loop will break.

    <category>
    <pattern>COUNT TO <set>number</set></pattern>
    <template>
      <think><set name="count">0</set></think>
      <condition name="count">
        <li><value><star/></value></li>
        <li>
          <set name="count">
            <map><name>successor</name><get name="count"/></map>
          </set>
          <loop/>
        </li>
      </condition>
    </template>
    </category>

>**Input:** Count to 6  
**Output:** 1 2 3 4 5 6

This example takes advantage of the built in set `number`, which verifies am input word as a number, and the built in map `successor`, which maps integers to their successive integers.

Before the condition block, the `count` predicate is initialized with the value `0`. If the user input was `Count to 0`, then the first list item will be returned (echoing the number found in the input).

Otherwise, the second item will be returned, and the `count` predicate is reset as the successive integer to the one found in the input. The loop element will run the condition again, and will continue to return the second list item until the predicate count matches the value of `<star />`.
