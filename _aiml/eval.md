---
layout: aiml
title: eval
---

### &lt;eval&gt;

The *eval element* is used to reference variables found in an outer category from within a nested category. This allows you to echo wildcard contents from an outer category from within a learn category.

Anything found within an eval element will be evaluated first, before the new category is created.

#### Usage

    <category>
    <pattern>THE * IS BLUE</pattern>
    <template>
      I will remember that the <star /> is blue.
      <learn>
        <category>
        <pattern>WHAT COLOR IS THE <eval><star /></eval></pattern>
        <template>The <eval><star /></eval> is blue</template>
        </category>
      </learn>
    </template>
    </category>

>**Input:** The sky is blue.  
**Output:** I will remember that the sky is blue.

>**Input:** What color is the sky?  
**Output:** The sky is blue.
