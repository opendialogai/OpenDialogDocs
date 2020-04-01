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

Intent can connect scenes by _spanning_ across scenes. moving forward the conversation. This can be achieved by the `scene` directive.

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

As mentioned above, each conversation must have at least one scene and this scene must be called `opening_scene`. The first incoming intents of this opening scene are known as opening intents. 

```yaml
conversation:
  id: example_conversation
  scenes:
    opening_scene:
      intents:
        - u:
            i: intent.app.opening_intent
        - u:
            i: intent.app.my_other_intent
        - b:
            i: intent.app_opening_intent_response
       ...
```

In this example either `intent.app.opening_intent` or `intent.app.my_other_intent` will be selected as the first incoming intent of example_conversation.

Out of the box, OpenDialog comes pre-configured with two such intents and conversations handling such intents are currently _expected_ for OpenDialog web-based chat to function as expected. The core opening intents are:

*   `intent.core.welcome`
*   `intent.core.NoMatch`


#### intent.core.welcome

This is the default intent that will be sent by OpenDialog webchat when a user opens the chat window. If you have a different intent that you would prefer to be used, you can update this in the Interpreter Engine configuration file by changing the mapping for the `WELCOME`callback.

```yaml
conversation:
  id: welcome_conversation
  scenes:
    opening_scene:
      intents:
        - u:
            i: intent.core.welcome
        - b:
            i: intent.app.welcome_response
       ...
```


#### intent.core.NoMatch

This is the intent that OpenDialog will send if it isn’t able to match a user’s utterance to any other possible incoming intent. This _no_match_conversation_ can be treated as the default catch-all conversation for a no match. However, if you use an intent.core.NoMatch within your own conversations those will take priority and allow you to provide more context specific no match messages back to the user. 

```yaml
conversation:
  id: no_match_conversation
  scenes:
    opening_scene:
      intents:
        - u:
            i: intent.core.NoMatch
        - b:
            i: intent.app.no_match_response
       ...
```


### Completing intents




### Virtual intents




### Repeating intents




## Interpreters




## Conditions




## Actions


