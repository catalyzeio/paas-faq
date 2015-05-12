---
title: SSL - PaaS FAQ
---

# SSL

### How do I update a SSL certificate?

Purchase a new certificate for your domain name from a SSL certificate provider. Verify the new certificate matches the domain name.  You can use [openssl](https://www.openssl.org/docs/) to view a x509 certificate that is in PEM format with the command `openssl x509 -in certficatefile -noout -text`. The results of the command will be  shown in your console.  Verify the new certificate and private key match. The section in our Onboarding documents regarding [Domain Names and SSL Certificates](https://resources.catalyze.io/paas/getting-started/deploying-your-first-app/domain-names/) contains more detailed information for verifying the key and certificate match as well as information about wildcard certificates and certificate chains.  Please contact Catalyze [support](https://catalyzeio.zendesk.com/hc/en-us/requests/new).   We will establish a secure method to share the files and schedule a time to update the certificate.