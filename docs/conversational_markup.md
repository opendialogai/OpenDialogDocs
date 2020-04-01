---
id: conversational_markup
title: Conversational Markup
---


## Conversations

Conversational design in OpenDialog relies on three key building blocks: **conversations**, **scenes** & **intents**. These three building blocks are in a hierarchical relationship where conversations contain scenes, and scenes contain intents. Within a single OpenDialog application there can be one or more conversations, with each conversation containing one or more scenes, and each scene containing one or more intents.

OpenDialog conversations model communication between two agents: a user and the OpenDialog application (otherwise referred to as a bot). In conversational design this communication is primarily modeled by a simple alternation between user and bot intents, however there is also scope for more complex patterns by using **interpreters**, **conditions** and **actions**.

Conversational markup in OpenDialog is defined using YAML, the basic structure of a conversation is as follows:

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
    second_scene:
      intents:
        - u:
            i: ...
        - b:
            i: ...
            completes: true
      ...
```


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


