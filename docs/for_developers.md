---
id: for_developers
title: OpenDialog for Developers
sidebar_label: OpenDialog for Developers
---

## OpenDialog for Developers

OpenDialog is a [Laravel](https://laravel.com) application with a MySQL backend for user management and content management and a [Dgraph](https://dgraph.com) backend (a graph-based database written in Go) for conversation management and conversational analytics. 

### Main Components

Below is a brief description of the main components of OpenDialog. 

- **Conversation Description Language** - this is a Yaml-based markup format that we use to describe conversations. The aim is to make it as simple as possible to describe potentially complex conversations that can deal with changing context and variations in user input.

- **Conversation Builder** - the conversation builder transforms that Yaml-based markup into a graph-based representation of a conversation that is stored in a graph database - we use [Dgraph](https://dgraph.com). It also helps the user to design _sensible_ conversations. By analysing the conversation it can identify potential pitfalls and suggest changes. 

- **Conversation Engine** - the conversation engine "runs" our conversations. It's the heart of OpenDialog. It determines, based on incoming utterances and overall state, what the next actions and outgoing messages should be.

- **Action Engine** - the action engine performs actions defined within conversations. It interfaces with the conversation engine and the context engine to update context and allow conversations to proceed taking into account the results of actions. Actions are the main way our conversational applications interface with external systems.


- **Context Engine** - the context engine keeps track of state. Through attributes we can store and retrieve information that is relevant to determining what actions and what messages we should perform. 

- **Response Engine** - the Response Engine takes an outgoing intent (in OpenDialog teminology this represents something the bot wants to say) and maps it to an actual message. The final message may change based on the channel it will be sent to and overall context.

- **Sensor Engine** - the Sensor Engine receives incoming messages and maps them to OpenDialog standard utterances and attributes and prepares them for consumption by the Conversation Engine. It is designed in a way that we can deal with multiple platforms (webchat, Slack, Alexa, etc).

- **Webchat Widget** - the Webchat Widget is a widget you can add to any website or web application and interact with an OpenDialog-powered chatbot. It provides a number of different message types and has a simple API to interact with as well as a rich set of configuration options. 









