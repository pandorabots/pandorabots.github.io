---
layout: aiml
title: that
---

### &lt;that&gt;

The *that element* is an optional child of the category element that is used to establish the context of the pattern. The bot is able to remember the last sentence it has said, and is defined as the value of "that".

If a category contains a *that element*, the pattern can only be matched if the last sentence of the bot's previous response matches the contents of `that`. In a sense, the *that element* binds a pattern to the immediate context of the conversation.

This is very useful for contextualizing common, simple user inputs such as "yes" or "no."

This allows you to have many duplicate patterns that, depending on the previous response, will trigger different templates.

The *that element* follows all the rules of the pattern element: The previous sentence given by your bot will be stripped of punctuation when read by a category referencing it with `<that>` tags. The new category will also ignore differences in capitalization/non-capitalized letters, and will expect any normalization you have specified in normal.substitution file.

For these reasons, we recommend you write the contents of the `<that>` tags like patterns: no punctuation, all capital letters, and normalized. If you are having trouble getting your `<that>` to work, usually it is one of those three items being amiss in your `<that>` tag.

Also note:  
* `<that>` tags can contain wildcards!
* Values for *that* variables are only within the scope of an active conversation. After some amount of idle time, the bot flushes context from memory.


#### Usage

    <category>
    <pattern>I LIKE COFFEE</pattern>
    <template>Do you take cream or sugar in your coffee?</template>
    </category>
    
    <category>
    <pattern>YES</pattern>
    <that>DO YOU TAKE CREAM OR SUGAR IN YOUR COFFEE</that>
    <template>I do too.</template>
    </category>
    
    <category>
    <pattern>NO</pattern>
    <that>DO YOU TAKE CREAM OR SUGAR IN YOUR COFFEE</that>
    <template>Really? I have a hard time drinking black coffee.</template>
    </category>

In the above example, we have accounted a possible conversation timeline, where the user initiates the conversation, and the bot responds by asking the user a yes or no question. The problem, however, is that there area near infinite number of questions the user may answer with "yes" or "no", so how does the bot know the context of the user's answer? Because the second and third categories contain that blocks, they are both bound to a particular context. These categories will not be matched unless the bot's previous response matches "DO YOU TAKE CREAM OR SUGAR IN YOUR COFFEE".

In this example below, it shows how to use the normalized version in your *that element*, assuming that you have the normal.substitution file normalizing *don't* to *do not*

    <category>
    <pattern>I LIKE TEA</pattern>
    <template>It's a civilized drink. Don't you agree?</template>
    </category>
    
    <category>
    <pattern>I DO</pattern>
    <that>DO NOT YOU AGREE</that>
    <template>My favorite is Lady Grey!</template>
    </category>
    

