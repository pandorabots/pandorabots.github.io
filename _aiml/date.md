---
layout: aiml
title: date
---

### &lt;date /&gt;

Returns the date of the user's locale.

#### Attributes

`format` (optional)  
Specifies the format of the returned date. This can be written like arguments to UNIX's `strftime` function. More on this [here](http://pubs.opengroup.org/onlinepubs/007908799/xsh/strftime.html).

#### Usage

    <category>
    <pattern>WHAT IS THE DATE</pattern>
    <template>Today is <date format="%B %d, %Y" /></template>
    </category>
