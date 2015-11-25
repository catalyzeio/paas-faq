---
title: Domains - PaaS FAQ
---

# Domains

### Can I have multiple domain names for an environment?

Yes, when configuring a new environment, you can add a domain name and SSL certificate with the Catalyze Dashboard.

If your environment is already configured, deployed and running please contact Catalyze support.  We will need to know the domain name and if the SSL certificate for the domain name will be a wildcard certificate. Someone from Catalyze will contact you so we can coordinate a schedule to make the change and establish a secure method of sharing the new certificate files.

### How do I change my environments domain name?

Please contact Catalyze [support](https://catalyzeio.zendesk.com/hc/en-us/requests/new) with the details of the new domain name.  We will need a SSL certificate that matches the domain name.  There are many providers of SSL certificates.  We will need to know the domain name and if the SSL certificate for the domain name will be a wildcard certificate.  Someone from Catalyze will contact you so we can coordinate a schedule to make the change and establish a secure method of sharing the new certificate files.

### How do subdomains work?

There are no limitations on subdomains. However with multiple root level domains, we do not currently provide functionality built into the dashboard to support this yet. If you need multiple root level domains you can file a ticket with support and we can add them for you. It's also worth noting that if you plan on using multiple subdomains you'll want a wildcard SSL Certificate (you should ask your certificate provider if they support SSL wildcard).
