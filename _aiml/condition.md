---
layout: aiml
title: condition
---

### &lt;condition&gt;

The *condition element* is used to create an IF-THEN-ELSE type of control flow within a bot's response. This is done by checking the value of a variable, and returning a response depending on that value.

#### Attributes

You can choose whether your condition rests on a predicate or local variable, depending on the attribute you provide:

`name`    
Specifies the name of the predicate whose value will be checked.

`var`    
Specifies the name of the local variable whose value will be checked.

#### Usage

The condition element is used in conjunction with list elements written with `value` attributes. If the value of the predicate referenced in the condition element matches that of any list element's value, that list element will be returned.

If the list element contains no value attribute, it will be returned in the case that no other list elements match the predicate's value.

    <category>
    <pattern>DO YOU FIND ME ATTRACTIVE</pattern>
    <template>
      <condition name="gender">
        <li value="male">I find you very handsome.</li>
        <li value="female">I find you very pretty.</li>
        <li>I find you very attractive.</li>
      </condition>
    </template>
    </category>

In this example, the bot will check the value of a predicate named `gender`. In the case that the predicate's value is either `"male"` or `"female"`, one of the first two list elements will be returned. If neither of these conditions is met, then the third list element will be returned.
