---
id: creating_a_conversation
title: Creating a Conversation
sidebar_label: Creating a conversation
---

A conversation is the key building block of an OpenDialog conversation application. When a user interacts with an app the first thing we do is determine what conversation we should _instantiate_ in order to manage the interaction. 

Conversations can have multiple _scenes_ and each scene can have multiple interactions. 

For the purposes of this guide, however, we will start with a simple conversation. Just a straightforward request-response. 

Here is the first one. It is the welcome conversation that comes out of the box with OpenDialog. You can see it by clicking on "Conversations" and then the welcome conversation.

```
conversation:
  id: welcome
  scenes:
    opening_scene:
      intents:
        - u:
            i: intent.core.welcome
        - b:
            i: intent.opendialog.WelcomeResponse
            completes: true

```

A conversation has a name, which is used to identify the conversation in the admin interface and a _model_ which is the Yaml representation of the conversation, follow OpenDialog's [conversational markup](conversation_markup.md).




The core unit of management of an OpenDialog bot is the conversation. 

It's worth [checking this out](conversational_model.md) to see how we think of conversations and the [conversational markup](conversation_markup.md) we use.

To add a conversation visit `admin/resources/conversations` and add a new conversation directly as a yaml definition. We are working on improving the overall validation process and further GUI support.

Once a conversation is save you need to publish it in order for it to be considered as a possible conversation for the bot to use. 

Also ensure that you provide outgoing messages that match the conversation's outgoing intents.  

  