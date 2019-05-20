---
id: adding_a_conversation
title: Adding a conversation
sidebar_label: Adding a conversation
---

The core unit of management of an OpenDialog bot is the conversation. 

It's worth [checking this out](conversational_model.md) to see how we think of conversations and the [conversational markup](conversation_markup.md) we use.

To add a conversation visit `admin/resources/conversations` and add a new conversation directly as a yaml definition. We are working on improving the overall validation process and further GUI support.

Once a conversation is save you need to publish it in order for it to be considered as a possible conversation for the bot to use. 

Also ensure that you provide outgoing messages that match the conversation's outgoing intents.  

  