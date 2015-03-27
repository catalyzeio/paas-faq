---
title: Application Related - PaaS FAQ
---

### How do I deploy my application?

After we provision your environment, we will provide you with a git URL to push your code to. You will receive [a Zendesk ticket](https://resources.catalyze.io/paas/getting-started/deploying-your-first-app/provisioning-your-environment/) update with those details. After you do your initial push to that git URL as outlined [here](https://resources.catalyze.io/paas/getting-started/deploying-your-first-app/deploying-the-app/). We will do the first deploy for you after which all subsequent deploys will be automatic. 

### How do I access my application after it has been deployed?

In the [email](https://resources.catalyze.io/paas/getting-started/deploying-your-first-app/provisioning-your-environment/) or ticket, all the details needed for you to access the application will be provided. Your Catalyze environment is configured with a public IP address, xxx.xxx.xxx.xxx. You can add a DNS record to your domain that will resolve to that public IP address. We also set up an alternate URL that will provide access to the application in the interim as well. That URL will be of the form - https://podxxxx.catalyze.io


### Do you have a cPanel?

We don't have a cPanel. The web interface we have for interacting with your Environment is the dashboard, which is accessibe [here](https://dashboard.catalyze.io). There you can change your environment variables and add ssh keys.

We also provide a command line interface that provides more interaction with your environment. You can download the catalyze-paas-cli [here](https://github.com/catalyzeio/catalyze-paas-cli). 


### Do you have a CLI?

We also provide a command line interface that provides more interaction with your environment. You can download the catalyze-paas-cli [here](https://github.com/catalyzeio/catalyze-paas-cli). More details on how to use the CLI is available [here](https://resources.catalyze.io/paas/getting-started/the-paas-cli/). The CLI is under active development and more and more features will be added over time. Note that it has also been open sourced so if you have any questions or issues, please do not hesitate to file an issue [there](https://github.com/catalyzeio/catalyze-paas-cli/issues). We would welcome contributions as well. Feel free to fork it and issue a pull request.

