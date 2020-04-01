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

Virtual intents allow you to _simulate_ an incoming intent in absence of an actual incoming intent from a user. You are essentially asking OpenDialog to behave _as if_ the user said something, without the user having said that. This can be useful if you wish to skip requiring the user to give input for some reason or, in general, where you can confidently skip a part of the conversation because of pre-existing contextual information. 

To specify a virtual intent, the `u_virtual` directive can be added to an outgoing intent containing the intent name to be simulated.

```yaml
conversation:
  id: create_task_conversation
  scenes:
    opening_scene:
      intents:
        - u:
            i: intent.app.createTask
        - b:
            i: intent.app.createTaskResponse
            scene: create_task_scene
    create_task_scene:
      intents:
        - u:
            i: intent.app.taskName
            interpreter: interpreter.app.taskName
            expected_attributes:
              - id: session.task_name
        - u:
            i: intent.app.noTaskName
            interpreter: interpreter.app.taskName
            scene: end_scene
        - b:
            i: intent.app.taskCreated
            scene: opening_scene
            u_virtual:
              i: intent.app.createTask
    end_scene:
      intents:
        - b:
            i: intent.app.endTaskCreation
            completes: true
```

For example in the above snippet, there is a conversation that allows a user to create a new task in a task management application. In `opening_scene` the user indicates they want to create a new task (`intent.app.createTask`) and the bot responds by explaining how to do so (`intent.app.createTaskResponse`), and the conversation moves to `create_task_scene`. In `create_task_scene`the user enters the task name (`intent.app.taskName`) and the bot responds to confirm that the task is now created (`intent.app.taskCreated`). At this point the scene directive moves the conversation back to `opening_scene` and the `u_virtual`directive sends the virtual `intent.app.createTask` intent. This means that the user does not need to send `intent.app.createTask` again, and the conversation skips straight to `intent.app.createTaskResponse` where the bot explains how to create a new task. It is worth noting that in this example there is a conversational loop, therefore it is important to have a way to break out of the loop which is offered by `intent.app.noTaskName`.


### Repeating intents




## Interpreters




## Conditions




## Actions


