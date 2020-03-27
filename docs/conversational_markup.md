---
id: conversational_markup
title: Conversational Markup
---


## Conversations




## Scenes




## Intents





### Opening intents




### Completing intents




### Virtual intents




### Repeating intents




## Interpreters




## Conditions




## Actions

If you have some functionality that should occur following the succesful identification and matching of an intent, you can associate that intent within the conversation to an _action_. Actions accept _input attributes_ and can return _output attributes_. Actions themselves are agnostic to the context’s that these attributes belong to (similar to how expected attributes work for [interpreters](conversational_markup.md#interpreters)).

Actions can be specified using the `action` directive, which contains an object with `id`, `input_attributes` & `output_attributes` properties.

```yaml
conversation:
  id: example_conversation
  scenes:
    opening_scene:
      intents:
        - u:
            i: intent.app.opening_intent
            action:
              id: action.core.example
              input_attributes:
                - user.first_name
                - user.last_name
              output_attributes:
                - user.full_name
        - b:
            i: intent.app_opening_intent_response
            completes: true
```

In the above snippet when `intent.app.opening_intent` is matched, OpenDialog will perform `action.core.example.` It takes input of the `first_name` and `last_name` attributes from the `user` context, and outputs a `full_name` attribute into the same context.
