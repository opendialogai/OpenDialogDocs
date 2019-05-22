---
id: attributes
title: Attributes
sidebar_label: Attributes
---

## What are attributes
Attributes are the way OpenDialog describes elements of the environment that the chatbot operates in that are required within conversational design and/or message content.

Attributes have a type (String, Int, Boolean, etc) and a value.

OpenDialog core defines a set of core attribute types but developers can add additional types based on their needs.

> For example, a user name can be represented with the attribute `name` of type `String`.

## Storing and retrieving attributes
Attributes are stored in _contexts_. Contexts are information stores that conform to the `Context` interface and provide a generic way for the ConversationEngine and the ResponseEngine to store or retrieve attributes. 

In order to identify in what context an attribute should be stored in we namespace attribute names. The format is `context_name.attribute_name`. Whenever OpenDialog encounters an attribute it will extract the attribute name and _resolve_ it - i.e. it will determine what type (Int, String, etc) is the attribute and then it will use the ContextManager to store or retrieve the attribute from an appropriate context. 

### Core Contexts
Out of the box OpenDialog suports the following contexts
- `user` - the user context stores attributes against the user node in Dgraph. 
- `session` - the session context is an in-memory context valid for a single request. 

We are planning to support other contexts such as `conversation` in future versions of OpenDialog.

### Custom Contexts
Developers can create custom contexts to store and retrieve relevant infromation. 

