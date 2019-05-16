---
id: conversational_applications
title: Conversational Applications
sidebar_label: Conversational Applications
---

## Conversational applications

**OpenDialog** is a framework for building and managing _conversational applications_ to automate, scale and improve processes and interactions within an organisation, between organisations and between an organisation and external users.

A _conversational application_ is an application whose main mode of interaction with the user is through the exchange of messages, which we call _utterances_. Each utterance carries an _intent_. An intent describes the underlying purpose of the party sending the _utterance_. That purpose or intent can be expressed using any number of different utterances ([Difference between utterances and intents](utterances_vs_intents.md)).

We refer to the task of mapping an utterance to an intent as _intent interpretation_.

The _**conversational engine**_ at the core of OpenDialog provides a way to describe what exchange of intents is useful or valid and provides tools to hook into intent interpreters so as to map utterances to those intents and extract other relevant information.

At the same time the conversational engine allows us to define _actions_ that should take place as a result of an intent being expressed. Actions are the things that will actually change something in the real world and fullfil the overall goal. For the example above the action would be that of creating a checklist for the user to use.

### Why do you call them conversational applications and not just chatbots?

We use the term _conversation application_ rather than chatbot because chatbot is very wide and, at times, misleading term. It's a bit like calling everything a website. Sure, on a given level _gmail.com_ and _nytimes.com_ are both websites but they serve very different purposes, have very different aims and are built with different sets of priorities governing them.

All conversational applications have chatbots-like characteristics but not all chatbots are conversational applications. We think of conversational applications as predominantly task-oriented. We worry less about being able to sustain any form of dialog or chit chat, or about having to somehow remain true to a _pure_ conversational paradigm where other types of widgets or tools cannot be introduced. The aim instead is to minimise the friction in getting tasks done over the appropriate channel (webchat, Slack, Alexa, Skype, etc) and automate as much of the underlying process as possible. The way the user communicates with the application happens to be predominantly conversationally-focussed but that does not preclude other interfaces being used whenever they can add more value than a conversation. 

Because actually performing actions is such an important part of a conversational application OpenDialog is  opinionated about how that takes place. As you will see, we provide specific support to interleave actions with conversation. In addition, we also focus on providing a solid semantic wrapper around everything so that we can always take advantage of context to pro-actively adjust behaviour. 

### Chatbots as intelligent agents

>OpenDialog takes an agent-based view of a chatbots.

Multi-agent systems development is a subfield of AI that studies the possible architecture of individual agents as well as the architecture of systems that allow multiple agents to coordinate towards both individual and joint goals.

OpenDialog models the interaction between the user and the chatbot as that between agents in a multi-agent system. In particular, we draw from work around around [electronic institutions](https://nms.kcl.ac.uk/michael.luck/resources/aij12.pdf) to describe the overall context within which users and bots operate in. In addition, we looked at [enhanced Dooley graphs](https://pdfs.semanticscholar.org/71e5/f7aee39470470c1bed39bf11790d8df4cccd.pdf) for the added flexibility in  representing the exchange of messages between participants in a conversation. 




