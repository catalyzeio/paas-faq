---
title: Databases - PaaS FAQ
---

# Databases

### What versions of the [supported databases](//resources.catalyze.io/paas/getting-started/deploying-your-first-app/supported-databases/) does Catalyze use?

- Percona 5.6
- PostgreSQL 9.3
- MongoDB 2.6

### How do database backups work?

We perform automated backups each night. If a user requires access to those backups we can provide them with the credentials to do so. We currently have plans in the works to add backup functionality to the dashboard.

### How do I get access to the database (or Redis or other) URL?
The endpoint connection information for the resources your application will consume is available in the environment variables for your environment.  You can view your environment variables in the Catalyze Dashboard or with the catalyze-paas-cli client program with the command:  `catalyze vars list`

You can download the CLI here - https://github.com/catalyzeio/catalyze-paas-cli. All associated install instructions are also available in the repo.

Note that this information will only be available *after* you have submitted the information required on the dashboard and we have provisioned your environment. This information will be accessible via an update to the Zendesk ticket.

### How I will deploy the database configuration?

There is a feature in the Catalyze command line interface (CLI) for importing a database.

```
>catalyze db --help
Usage: catalyze db [OPTIONS] COMMAND [ARGS]...

  Interact with database services.

Options:
  --help  Show this message and exit.

Commands:
  import  Imports data into a database

 ```

 If you run into issues with this, please file a support ticket [here](mailto:support@catalyze.io). We can, if really need be, import the data for you. Please DO NOT send the dump via zendesk or other channels, especially if the data contains PHI. We will create a Box folder and share that with you. We will also need the specific command which you need to be run to import the data as well.

### How I can change the database configuration?

Either with your code or we can setup a command line bastion service that will allow you to connect to the database client application via ssh. We're working on a secure console access which will eliminate the need for a bastion service. Note that there might be a cost for the bastion service. Please file a support ticket if you would like this added to your environment. Please note that this access is not available in the startup plan.


### What will be the database connection string that I can use inside the application?

Your Catalyze environment has the environment variables for the database (along with other relevant variables such as Redis, sentinel or arbiter URLs) specified in [a Zendesk ticket](https://resources.catalyze.io/paas/getting-started/deploying-your-first-app/provisioning-your-environment/) update that you would have received. Your application can read these and setup the connection based on that information.

### I have a database bastion service. How do I connect to the DB bastion ?

When your database bastion service was configured and deployed, you should have received a message from Catlayze Support that informed you have the user name and ssh key that should be used to connect to the service.

Use a ssh client, such as openssh or putty to remotely connect to the database client application.

To connect with openssh, enter the ssh command in the format  `ssh -i <identify file> <user>@<ip address>`.  For example `ssh -i /home/fred/mykeys/catalyze.key fred@104.101.102.103`

### How does database promotion take place if the primary fails or if we need to promote manually?

Our HA database is configured as a master-slave setup, it's up to your application to manage which one to connect to. You can also contact us if you need something manually promoted to master by filing a support ticket.

