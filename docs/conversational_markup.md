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

Conditions can be used to ensure that only specific intents are considered for matching. They can be specified by using the `conditions` directive, which must contain an array of `condition` objects. If multiple conditions are given for a single intent they are combined on an `AND` basis. Conditions can used on both incoming and outgoing intents, however their behaviours differ slightly.

Conditions on incoming intents are evaluated after interpretation, which means that OpenDialog will have interpreted the user's utterance (but not yet have matched to an incoming intent). The conditions of these potential intents are then evaluated, with the first passing intent being selected. This allows conversation designers to specify conditions using attributes of the interpreted intents. This can be done by using the built-in `_intent` context which will be temporarily populated with the expected attributes of the intent.

For outgoing intents, conditions are evaluated first. Conditions are the only way to instruct OpenDialog to choose between a consecutive grouping of outgoing intents.

```yaml
conversation:
  id: example_conversation
  scenes:
    opening_scene:
      intents:
        - u:
            i: intent.app.opening_intent
            scene: appropriate_price_scene
            interpreter: interpreter.core.luis
            confidence: 0.75
            expected_attributes:
              - id: item.price
            conditions:
              - condition:
                  operation: gte
                  attributes:
                    attribute: _intent.price
                  parameters:
                    value: 10
              - condition:
                  operation: lte
                  attributes:
                    attribute: _intent.price
                  parameters:
                    value: 50
        - u:
            i: intent.app.opening_intent
            interpreter: interpreter.core.luis
            confidence: 0.75
            expected_attributes:
              - id: item.price
       ...
```

In the above snippet there are two instances of `intent.app.opening_intent`, both of which use the LUIS interpreter and expect a `price` attribute. If the `price` attribute value is greater than or equal (`gte` operation) to 10 and less than or equal (`lte` operation) to 50, then the user will be taken into `appropriate_price_scene`, otherwise they will remain in `opening_scene`.

## Actions


