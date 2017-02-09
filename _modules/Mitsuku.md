---
layout: default
title: Mitsuku
---

# Mitsuku 

The Mitsuku Module is a bot module ported from the award-winning [Mitsuku chatbot](http://www.mitsuku.com/). It was designed as an integration in a bot network, to serve as a personality layer or general knowledge/conversational back-end. Bot modules abstract a lot of the work that goes into creating a robust, fully-featured chatbot system.

Use of the Mitsuku Module is available as a premium add-on to select [AIaaS plans](https://developer.pandorabots.com/#plans). *Please contact [info@pandorabots.com](info@pandorabots.com) for pricing and additional details.*

## Credentials

Following purchase and setup, you will receive a custom set of credentials required to make calls to the Mitsuku Module. These can be retrieved from your application details page at [chatbots.io](https://developer.pandorabots.com/), as Mitsuku Module.

You should store these as a bot property in your bot’s .properties file:

`[["mitsukumodule", "<Mitsuku Module Credentials>"]]`

## Routing to Mitsuku

In order to integrate the Mitsuku Module with your bot, you’ll have to include some AIML to route inputs from your users. The `<sraix>` element tells your bot to send some text to another bot on the server:

    <!-- mitsukumodule request handler from routes.aiml -->
    <category>
      <pattern>XMITSUKUMODULE *</pattern>
      <template><srai>XMITSUKUMODULE XRESPONSE <sraix><bot><bot name="mitsukumodule"/></bot><star/></sraix> XENDX</srai></template> 
    </category>

    <!-- mitsukumodule response handlers from routes.aiml -->
    <category>
      <pattern>XMITSUKUMODULE XRESPONSE * XENDX</pattern>
      <template><star/></template>
    </category>

The routing category determines how your bot will decide when to send an input to the Mitsuku Module.

    <!-- ultimate default category from pand_system.aiml -->
    <category>
      <pattern>*</pattern>
      <template><srai>XMITSUKUMODULE <star/></srai></template>
    </category>

In this basic example, the Mitsuku Module is attached to the default category. Whenever your bot fails to find a better match for an input, this category will be matched. If this was the only category contained by your bot, everything you say to it would automatically redirect to the module.

You can target more specific inputs by using context and pattern-matching. For example, you could use the topic tag to forward all soccer related conversation to the Mitsuku Module:

    <topic name="soccer">
    <category>
      <pattern>*</pattern>
      <template><srai>XMITSUKUMODULE RESPONSE <sraix><bot><bot name="mitsukumodule"></bot><star/></sraix> XENDX</srai></template>
    </category>
    </topic>

## Name override (OPTIONAL)

You can override the Mitsuku Module’s name by wrapping the <sraix> element described above in the <denormalize> tag:

    <!-- Modified request handler for mitsukumodule in routes.aiml -->
    <category>
      <pattern>XMITSUKUMODULE *</pattern>
      <template><srai>XMITSUKUMODULE XRESPONSE <denormalize><sraix><bot><bot name="mitsukumodule"/></bot><star/></sraix></denormalize> XENDX</srai></template>
    </category>

Then, modify the denormal.substitutions file to include the following key-value pair as a substitution (use your intended name as the second item):

    [
    ["Mitsuku", "Alice"],
    :
    ]

Now, any time the module returns some text that contains the word Mitsuku, the denormalize tag will replace the word with the name you specified. 

Please note that while you can override her name in this manner, the Mitsuku personality is not changeable. She will continue to be a young woman from the UK with a sassy personality regardless of the name change! 

## Custom response handling (OPTIONAL)

You also have the option to intercept a response from Mitsuku module before it is returned to your end user. This allows you to give your bot different behavior depending on what the module returns:

    <!-- mitsukumodule request handler from routes.aiml -->
    <category>
      <pattern>XMITSUKUMODULE *</pattern>
      <template><srai>XMITSUKUMODULE XRESPONSE <sraix><bot><bot name="mitsukumodule" /></bot><star/></sraix> XENDX </srai></template>
      </category>

From the initial routing AIML described above, you’ll notice that the `<sraix>` route to the Mitsuku Module is wrapped in an `<srai>` tag. This allows you to redirect module’s response to another category in your bot, for additional processing before a response is returned to the user. We’ve prepended the string XMITSUKUMODULE to mark inputs that have been received by Mitsuku Module.

    <!-- "response handler" in routes.aiml -->
    <category>
      <pattern>XMITSUKUMODULE XRESPONSE * XENDX</pattern>
      <template><star/></template>
    </category>

This category will now capture all responses returned by the module. You can then write additional patterns beginning with XMITSUKUMODULE to capture certain responses. For example, to handle a recursion error gracefully:

    <category>
      <pattern>XMITSUKUMODULE XRESPONSE TOO MUCH RECURSION IN AIML XENDX</pattern>
      <template>I’m sorry, I am pretty busy right now.</template>
    </category>

    <category>
      <pattern>SRAIXFAILED</pattern>
      <template>I’m sorry, I am pretty busy right now.</template>
    </category>

## Predicates

For information on getting and setting predicates in your own bot, please take a look at our [tutorial](http://docs.pandorabots.com/tutorials/predicates/) on the subject.

Predicates can be stored in either your own bot or in Mitsuku, however, the two bots will not have direct access to each other’s variables. This prevents a bot from “leaking” information about its user to other bots. All variables will be resolved locally in a bot before a string is passed to another bot via `<sraix>`.

The Mitsuku Module contains a wealth of AIML that sets predicates during conversation, mostly regarding personal details about the end user (age, location, gender, etc.). You can issue the input “CLIENT PROPERTIES” to Mitsuku Module to get client predicates it currently has stored.

## Properties

The hardwired properties of the Mitsuku Module can also be displayed by entering bot input "BOT PROPERTIES".

## Next Steps

Email info@pandorabots.com for pricing and additional support questions during setup.
