---
layout: aiml
title: id
---

### &lt;id /&gt;

The *id element* returns the current `botid`, along with the `client_name` of whoever has issued the input. `botid` is the same as `app_id/botname`.

#### Usage

Here is an example of using the `<id/>` tag on the Playground, inside of a bot with
the app_id "Daniel" and botname "test":

    <category>
      <pattern>TEST ID</pattern>
      <template><id/></template>
    </category>

>**Input:** TEST ID  
**Output:** -playground-daniel/test/daniel
