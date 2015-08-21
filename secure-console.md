---
title: Secure Console
---

Catalyze Secure Console
=======================

The Secure Console command will be the entry point for you to dive into your application's environment. With it you can attach to a PostgreSQL, MySQL, or MongoDB database shell or start up a Rails or Django console. The Secure Console also brings added flexibility allowing you to execute commands and get the output back in your terminal. At a high-level it works by starting up a new container within the environment's network and allowing your terminal to interact with the container over a secure websocket. The console container is then able to connect to the requested service and perform the task. 

```
$ catalyze console --help
Usage: catalyze console service [command]
…
```

In the general usage of the command you must specify the name of the service for the console to connect to followed by an optional command to initiate when the console is opened. If connecting to a database shell only the service name required, the command string should be left blank. The following are several examples to get you started with the secure console command.

Connect to a database shell (database service named "db01"):

```
$ catalyze console db01
```

Connect to the Rails Console (application service named "app01"):

```
$ catalyze console app01 'bundle exec rails console'
```

or the Django Shell (application service named "app01"):

```
$ catalyze console app01 'python manage.py shell'
```

With the console command you can also run single commands and receive the command output back to your terminal. Try kicking off migrations in your Django app:

```
$ catalyze console app01 'python manage.py migrate'
```

### The command I want to run is complaining about not being whitelisted, how can I get it added to the whitelist?
The Catalyze Platform team maintains a whitelist of secure console commands in order to maintain the integrity and security of the platform for all of its users. We may add commands to the whitelist on an as-needed basis or as we add new features to the platform. Our goal is to enable you accomplish the tasks you need while adhering to stringent security standards. Please reach out to us at support@catalyze.io if your command is not included in the current whitelist. 
