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

Whereas outgoing intents can be deterministically mapped to message templates, the mapping from a user’s utterance to an incoming intent requires interpretation. For this we can use OpenDialog Interpreters. Interpreters take input in the form of an utterance (eg. text, button value, form, etc) and output an intent with a confidence score and optional attributes.

By default OpenDialog sets `interpreter.core.callbackInterpreter`as the default interpreter for all incoming intents. This means that if you would like the Callback Interpreter to interpret an intent, you do not need to specify it. If you would like interpretation to be carried about by a non-default interpreter, you must specify it on an outgoing intent by using the `interpreter` directive.

 The `confidence` directive can be used to indicate a minimum confidence score that the interpreter must produce for the given intent to match. If this directive is omitted, it will default to 1 which means that the interpreter will have to be 100% certain that the given intent matches.

The interpreted intent can also be told to store attributes from the interpretation by specifying the `expected_attributes` directive. This can take an array of attribute names prefixed by a context name.

```yaml
conversation:
  id: example_conversation
  scenes:
    opening_scene:
      intents:
        - u:
            i: intent.app.opening_intent
            interpreter: interpreter.core.luis
            confidence: 0.75
            expected_attributes:
              - id: session.first_name
        - b:
            i: intent.app_opening_intent_response
            completes: true
```

In the snippet above `intent.app.opening_intent` is interpreted by the built-in Microsoft LUIS Interpreter (`interpreter.core.luis`).  In this example `intent.app.opening_intent` can include a `first_name` attribute, which the markup specifies should be stored in the context called `session`. If LUIS returned a confidence lower than 0.75, `intent.app.opening_intent` **would not** be matched and OpenDialog would instead match [`intent.core.NoMatch`](conversational_markup.md#intentcorenomatch).


## Conditions




## Actions


