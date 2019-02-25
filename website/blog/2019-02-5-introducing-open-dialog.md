---
title: Introducing OpenDialog
author: Ronald Ashri
authorURL: http://twitter.com/ronald_istos
---

## What is OpenDialog?

OpenDialog is an open-source conversation management framework being built by [GreenShoot Labs](https:://greenshootlabs.com). 

We aim to build a tool that:

- Makes it easy to design and manage conversations while allowing for very flexible flows.
- Makes conversational flows and patterns shareable across different applications.
- Makes it simple for both small and large teams to collaborate.
- Provides a robust deployment process that can support simple applications but also more complex organisational and editorial flows.
- Is scalable and can be used with other tools and technologies.
- Is flexible in allowing you to choose how to interpret user utterances, with the ability to combine different tools in a single application and even throughout a single conversation (from your own NLP tooling to cloud-based services to simple regular expressions). 
- Provides a range of plugins that allow you to easily take advantage of cloud-based NLP tools (Luis.ai, Dialogflow, Amazon Comprehend, etc.) as well as other open-source tools (Rasa, spaCy, etc.).

## Why build (yet another) conversation management framework?

There are plenty of tools out there to manage conversations, from SaaS-based solutions to open-source solutions. Many of these tools are amazing and an inspiration to us. The field, however, is incredibly young and ideas and approaches are still developing rapidly. We have not converged on a set of patterns and best practices around how to build conversational applications.

Through OpenDialog we are making our thinking around the subject available to add to the broader conversation. We see real merit in the approach we've taken and open-sourcing the tool means that it can inform the wider debate and provide us with feedback on our ideas.

## What problems is OpenDialog trying to solve

At its core, OpenDialog is trying to solve three challenges.

1. How can we think about, design, implement and re-use non-trivial conversational patterns consistently and coherently?
2. How do we connect conversation to action, integrate with other systems and have a standard way of describing and engineering the whole?
3. How can we support large teams as they collaborate to build services with conversational interfaces and support a variety of editorial flows for conversations?

Some of the user stories we are explicitly considering are: 

1. As a conversation manager, I want to manage conversations and the content of the conversations without needing developers to change the code constantly. 
2. As a conversation designer, I want to test different conversation ideas and be able to change my mind and roll back on conversations both in a test environment and on a production environment.
3. As a developer, I want to implement integrations into other services and build more extensive application flows that cleanly include the conversational aspect in a scalable way that separates concerns. 
4. As a developer, I want to be able to re-use solutions across different domains and identify broad execution patterns in a conversational context.
4. As a product owner, I want to keep track of the performance of my conversational application as conversations evolve.

## Where is OpenDialog now?

OpenDialog is the second iteration of our conversational management tool. We are taking a bunch of lessons from the past 12 months and turning them into a more sustainable and better-engineered tool that can be shared widely. 

All of the development (of boths ideas and code) will be done on [Github](https://github.com/greenshootlabs/opendialog) and on this website. 

## What's the tech stack like?

At it's core OpenDialog is built on top of the Laravel framework. It will start out as a Laravel package and then develop into a full Laravel application.

We have a conversation markup language to describe conversations in yaml and a message markup language to manage messages for different conversational interfaces.

We provide our own front-end webchat component using Vue.js

The conversation engine uses [Dgraph](https://dgraph.io) to store and traverse conversation graphs (more about these in the next blog post), contextual information, and log conversations for subsequent analysis.


## Ok - so how do I keep up?

We will be regularly sharing pieces of the work as it is ready for wider consumption. If you are in London come to the February Chatbot [meetup](https://www.meetup.com/Messaging-Bots-London/events/257034547/) - we will be there talking about and demonstrating OpenDialog.

Follow us on [Twitter](https://twitter.com/greenshootlabs) or [LinkedIn](https://www.linkedin.com/company/greenshoot-labs/) or drop us an email at hello@greenshootlabs. We are more than happy to jump on a call and show you what we have so far and get comments. 

