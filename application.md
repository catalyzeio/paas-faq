---
title: Application Related - PaaS FAQ
---

# Application


### How do I deploy my application?

After we provision your environment, we will provide you with a git URL to push your code to. You will receive [a Zendesk ticket](https://resources.catalyze.io/paas/getting-started/deploying-your-first-app/provisioning-your-environment/) update with those details. After you do your initial push to that git URL as outlined [here](https://resources.catalyze.io/paas/getting-started/deploying-your-first-app/deploying-the-app/). We will do the first deploy for you after which all subsequent deploys will be automatic.


### How do I access my application after it has been deployed?

In the [email](https://resources.catalyze.io/paas/getting-started/deploying-your-first-app/provisioning-your-environment/) or ticket, all the details needed for you to access the application will be provided. Your Catalyze environment is configured with a public IP address, xxx.xxx.xxx.xxx. You can add a DNS record to your domain that will resolve to that public IP address. We also set up an alternate URL that will provide access to the application in the interim as well. That URL will be of the form - https://podxxxx.catalyze.io


### Do you have a cPanel?

We don't have a cPanel. The web interface we have for interacting with your Environment is the dashboard, which is accessible [here](https://dashboard.catalyze.io). There you can change your environment variables and add ssh keys.

We also provide a command line interface that provides more interaction with your environment. You can download the catalyze cli here: [here](https://github.com/catalyzeio/cli).


### Do you have a CLI?

We also provide a command line interface that provides more interaction with your environment. You can download the catalyze cli [here](https://github.com/catalyzeio/cli). More details on how to use the CLI is available [here](https://resources.catalyze.io/paas/getting-started/the-paas-cli/). The CLI is under active development and more and more features will be added over time. Note that it has also been open sourced so if you have any questions or issues, please do not hesitate to file an issue [there](https://github.com/catalyzeio/cli/issues). We would welcome contributions as well. Feel free to fork it and issue a pull request.


### Do I have access to Cloud Storage?

As part of your Catalyze environment you have a fixed amount of "Cloud Storage" space that includes your application's assets (the application code/binaries, static JavaScript, HTML, CSS) as well as disk space used by your database instance. This is not the same as a cloud-based file storage or CDN solution like Rackspace's Cloud Files or AWS S3.

We have the ability to configure a compliant S3 bucket as part of you environment at an additional charge. This is our preferred approach, as opposed to storing content like large images and PDFs in your git repository (which is considered bad practice by most) and then serving them up via your application. Please [contact us](https://catalyzeio.zendesk.com/hc/en-us/requests/new) for details.


### How do I send email? Is there a SMTP server?

The Catalyze Platform does not provide a SMTP service.
Ultimately you do not want to send PHI in email. Best practice recommends you prompt users to log into your application to view their data there.

To conduct simple email communication that does not include PHI, Mailgun, Mandril or Google Apps are examples of email handling services you could use.


### Can I connect to my PaaS environment via a VPN?

We do not support the ability to connect to PaaS environments via VPN. We are able to configure secure console access via SSH to meet certain use cases. This service requires an additional monthly charge. Please [contact us](https://catalyzeio.zendesk.com/hc/en-us/requests/new) for details.

Beyond that, all interaction with your PaaS environment should be done with the [Catalyze Dashboard](https://dashboard.catalyze.io), Catalyze [paas-cli](https://github.com/catalyzeio/cli) client application or your application code.


### Are any metrics available for my Paas environment?

We are currently working on a solution that will provide access to the metrics used by your PaaS environment through the CLI and the dashboard. This feature is in beta and will be available to all users via the CLI by mid-Summer 2015. Dashboard integration will follow soon after.

To get a preview of the type of metrics we are collecting, have a look at our [cadvisor-metrics](https://github.com/catalyzeio/cadvisor-metrics) repository, which we wrote specifically for this purpose and have released as open source software.


### How do I schedule tasks for my application?

Oftentimes in your application you'll want to schedule a task that runs periodically or at a specific time throughout the day/week/month/etc. This sounds like I'm describing the `cron` utility... However, `cron` (or a `cron`-like service) may not be the best option for your application. If you rely on scheduled tasks getting executed on-time and successfully we recommend moving this behavior within the control of your application. There are many task scheduling frameworks available to easily fit inside of your application. These generally have advantages over cro:wqn-like services which offer the ability to scale, have improved restart behavior, and retry failed tasks all to improve the guarantee that your tasks will run.

Some of our recommended task scheduling frameworks include [Sidekiq](https://github.com/mperham/sidekiq/wiki) for Ruby and [Celery](http://www.celeryproject.org) for Python. These scheduling frameworks are generally backed by a message broker such as Redis or an AMQP-based alternative like Rabbitmq which helps guarantee message delivery.

Currently the Catalyze Platform does not offer a `cron`-like service for production ready applications. But fear not! We have a few features percolating and hopefully be ready for you to plug into soon!
