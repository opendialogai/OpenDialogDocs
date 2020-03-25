---
id: installing_opendialog
title: Installing OpenDialog
sidebar_label: Installing OpenDialog
---


## Introduction

OpenDialog is a Laravel web application that uses two database services. Standard MySQL for user management (people who can administer the chatbot) and configuration and Dgraph for storing conversations. 

### Lando-based Quickstart Installation

Currently, the most effective way to install OpenDialog is to make use of our Lando-based quickstart installation. Lando is a wrapper around docker services and means you don't have to deal with any configuration in your local environment other than installing Lando itself. 


- Install [Lando](https://docs.devwithlando.io/installation/system-requirements.html) -- Lando is a wrapper around Docker services and it brings together everything that is required for OpenDialog.

- Run the setup script: 

```bash ./scripts/set_up_od.sh {appname}```

 where {appname} is the name of the app. 

 On initial setup you will be prompted to clear your local Dgraph and conversations. Select yes.

- Your app will be available at: https://{appname}.lndo.site/admin

Notes: 

- You may need to permanently trust the ssl cert, you can find this at ~/.lando/certs/lndo.site.crt


Once installation has completed you can login using the default credentials:

```admin@example.com / opendialog```

Go to > Test Bot
Ask the Bot anything.
You should see the no-match message.

- The DGraph browser will be available here: https://dgraph-ratel.lndo.site

- DGraph Alpha should be available at https://dgraph-alpha.lndo.site