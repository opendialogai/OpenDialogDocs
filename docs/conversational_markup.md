---
id: conversational_markup
title: Conversational Markup
---


## Conversations




## Scenes




## Intents





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


