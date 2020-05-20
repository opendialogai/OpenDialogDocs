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

To allow users to move from one conversation to another, each conversation must eventually end. This can be achieved by denoting completing intents using the `completes` directive. Completing intents are intents that once matched, will end the current conversation.

```yaml
conversation:
  id: example_conversation
  scenes:
    opening_scene:
      intents:
        - u:
            i: intent.app.openingIntent
        - b:
            i: intent.app.openingIntentResponse
            completes: true
```


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
