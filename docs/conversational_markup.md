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

Virtual intents allow you to simulate an incoming intent in absence of an actual incoming intent from a user. This can be useful if you wish to skip requiring the user to give input for some reason. To specify a virtual intent, the `u_virtual` directive can be added to an outgoing intent containing the intent name to be simulated.

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
            interpreter: interpreter.app.task_name
            expected_attributes:
              - id: session.task_name
        - u:
            i: intent.app.no_task_name
            interpreter: interpreter.app.task_name
            scene: end_scene
        - b:
            i: intent.app.task_created
            scene: opening_scene
            u_virtual:
              i: intent.app.create_task
    end_scene:
      intents:
        - b:
            i: intent.app.end_task_creation
            completes: true
```

For example in the above snippet, there is a conversation that allows a user to create a new task in a task management application. In `opening_scene` the user indicates they want to create a new task (`intent.app.create_task`) and the bot responds by explaining how to do so (`intent.app.create_task_response`), and the conversation moves to `create_task_scene`. In `create_task_scene`the user enters the task name (`intent.app.task_name`) and the bot responds to confirm that the task is now created (`intent.app.task_created`). At this point the scene directive moves the conversation back to `opening_scene` and the `u_virtual`directive sends the virtual `intent.app.create_task` intent. This means that the user does not need to send `intent.app.create_task` again, and the conversation skips straight to `intent.app.create_task_response` where the bot explains how to create a new task. It is worth noting that in this example there is a conversational loop, therefore it is important to have a way to break out of the loop which is offered by `intent.app.no_task_name`.


### Repeating intents




## Interpreters




## Conditions




## Actions


