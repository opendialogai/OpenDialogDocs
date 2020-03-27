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

Repeating intents enable a set of intents to loop. An incoming intent that is marked with the `repeating` directive will be matched as per usual, however after the bot has replied with its outgoing intent, the conversation will be reset to the position it was prior to the repeatable incoming intent.

```yaml
conversation:
  id: create_task_conversation
  scenes:
    opening_scene:
      intents:
        - u:
            i: intent.app.create_task
        - b:
            i: intent.app.create_task_response
            scene: create_task_scene
    create_task_scene:
      intents:
        - u:
            i: intent.app.task_name
            repeating: true
            interpreter: interpreter.app.task_name
            expected_attributes:
              - id: session.task_name
        - u:
            i: intent.app.no_task_name
            interpreter: interpreter.app.task_name
            scene: end_scene
        - b:
            i: intent.app.task_created
    end_scene:
      intents:
        - b:
            i: intent.app.end_task_creation
            completes: true
```

In the above snippet the `intent.app.task_name` intent is a repeated intent. When a user sends `intent.app.task_name`, the bot replies (as usual) with `intent.app.task_created`, however after this the conversation will then jump back to its state prior to receiving the user’s incoming intent. The next valid intents will again be `intent.app.task_name` or `intent.app.no_task_name`, and this can be repeating over and over until `intent.app.no_task_name` is sent by the user.


## Interpreters




## Conditions




## Actions


