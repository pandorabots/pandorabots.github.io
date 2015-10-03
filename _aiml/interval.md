---
layout: aiml
title: interval
---

### &lt;interval&gt;

The *interval element* is used in conjunction with the date element to calculate the difference between two different times/dates.

#### Attributes

`format`  
Specifies the format of the returned date. This can be written like arguments to UNIX's `strftime` function. More on this [here](http://pubs.opengroup.org/onlinepubs/007908799/xsh/strftime.html).

#### Child tags

`<from>`  
Specifies the date from which the interval should begin.

`<to>`  
Specifies the date at which the interval should end.

`<style>`  
Specifies the style in which the interval should be returned. Can contain `years`, `months`, `days`, or `seconds`.

#### Usage

To calculate the difference between the current date and the bot's birthdate, make sure to include a birthdate property in the `.properties` file, in a format that matches the format you intend to be working with.

    <category>
    <pattern>AGE IN YEARS</pattern>
    <template>
      <interval format="%B %d, %Y">
        <style>years</style>
        <from><bot name="birthdate"/></from>
        <to><date format="%B %d, %Y" /></to>
      </interval>
    </template>
    </category>

The style element specifies that the interval should be returned in years.
