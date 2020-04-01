---
id: conversational_markup
title: Conversational Markup
---


## Conversations




## Scenes

Scenes are groupings of intents within a conversation. Each conversation is required to have at least one scene and this scene **must** be called `opening_scene`. This lets OpenDialog know which scene to select first when entering a new conversation. The first incoming intents within this opening scene are called [opening intents](conversational_markup#opening-intents) (we will be discussing them in more detail in the next sections). 

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
            completes: true
```


## Intents





### Opening intents




### Completing intents




### Virtual intents




### Repeating intents




## Interpreters




## Conditions




## Actions


