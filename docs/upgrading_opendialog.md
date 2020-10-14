---
id: upgrading_opendialog
title: Upgrading OpenDialog
sidebar_label: Upgrading OpenDialog
---


## Introduction

Upgrading OpenDialog should generally be a similar process to upgrading any Laravel application. We do aim, however, to provide detailed upgrade instructions here once OpenDialog is on a more stable release schedule, especially where there may be breaking changes in the graph schema or the interfaces for the core OpenDialog conversational framework. 

In the meantime we offer some general pointers that we use for guiding the upgrade process.

## Backup all data 

Make sure all data is save as depending on the state of your own application and Dgraph there may information that will not smoothly migrate to further versions. 

You can export conversation templates and messages through an Artisan commands. 

`php artisan conversations:export`


## Upgrade the OpenDialog application

Get the version of the OpenDialog application for the [repository](https://github.com/opendialogai/opendialog) and merge it into your own application. 

If you haven't changed any core OpenDialog elements you are only likely to see merge conflicts in areas such as your composer.json. Ensure that you are adhering to all the version requirements for the OpenDialog app, resolve conflicts and do a `composer update`. This will pull in the latest versions of OpenDialog Core and OpenDialog webchat.

Then make sure to do a 

`php artisan migrate` for any database tables and data migrations.

## Follow any Laravel framework upgrade instructions

Depending on what Laravel framework upgrade has taken place following the upgrade of the OpenDialog application check out the [Laravel upgrade](https://laravel.com/docs/6.x/upgrade)

## Upgrade your bot

Your own bot may be using custom Attributes, Actions, Interpreters and Contexts - make sure you check for any interface updates to how those elements are defined and match those changes in your domain-specific implementations. 


## Test your conversations

Finally, test your conversations to ensure that the bot is behaving as expected! 