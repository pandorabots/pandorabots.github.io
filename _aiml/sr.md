---
layout: aiml
title: sr
---

### &lt;sr /&gt;

The *sr element* is shorthand for `<srai><star /></srai>`. Because this is one of the most often-used combinations of elements, AIML allows you to write as a shortened version.

#### Usage

Use anywhere you'd like to reduce an input with a single wildcard to the wildcard contents. For example, the two following patterns are the same, in practice:

    <category>
      <pattern>FAVORITE *</pattern>
      <template><srai><star/></srai></template>
    </category>

    <category>
      <pattern>FAVORITE *</pattern>
      <template><sr/></template>
    </category>
