---
id: conversational_markup
title: Conversational Markup
---


## Conversations




## Scenes




## Intents





### Opening intents




### Completing intents

To allow users to move from one conversation to another, each conversation must eventually end. This can be achieved by denoting completing intents using the `completes` directive. Completing intents are intents that once matched, will end the current conversation.

```yaml
conversation:
  id: example_conversation
  scenes:
    opening_scene:
      intents:
        - u:
            i: intent.app.openingIntent
        - b:
            i: intent.app.openingIntentResponse
            completes: true
```


### Virtual intents




### Repeating intents




## Interpreters




## Conditions




## Actions


