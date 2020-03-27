---
id: conversational_markup
title: Conversational Markup
---


## Conversations




## Scenes




## Intents

Intents come in two forms: incoming & outgoing. Incoming intents are interpreted from a user’s utterance, whereas outgoing intents are matched by conversational logic and mapped to a message template.

```yaml
conversation:
  id: example_conversation
  scenes:
    opening_scene:
      intents:
        - u:
            i: intent.app.opening_intent
        - b:
            i: intent.app_opening_intent_response
       ...
```

In the snippet above `intent.app.opening_intent` is an incoming intent from the user, signified by the `u`, and `intent.app.opening_intent_response` is an outgoing intent from the bot, signified by the `b`.

One purpose of an intent is to move the conversation from one scene to another. This can be achieved by the `scene` directive.

```yaml
conversation:
  id: example_conversation
  scenes:
    opening_scene:
      intents:
        - u:
            i: intent.app.opening_intent
        - b:
            i: intent.app_opening_intent_response
            scene: second_scene
    second_scene:
      intents:
        - u:
            i: intent.app.closing_intent
        - b:
            i: intent.app.closing_intent_response
            completes: true
```

In the snippet above when the bot responds with `intent.app_opening_intent_response`, the conversation moves from `opening_scene` to `second_scene`.

Intents can also have additional directives which will be explained in the sections below.


### Opening intents




### Completing intents




### Virtual intents




### Repeating intents




## Interpreters




## Conditions




## Actions


