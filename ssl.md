---
title: SSL - PaaS FAQ
---

# SSL

## How do I update a SSL certificate?

Purchase a new certificate for your domain name from a SSL certificate provider. Verify the new certificate matches the domain name.  You can use [openssl](https://www.openssl.org/docs/) to view a x509 certificate that is in PEM format with the command `openssl x509 -in certficatefile -noout -text`. The results of the command will be  shown in your console.  Verify the new certificate and private key match. The section in our Onboarding documents regarding [Domain Names and SSL Certificates](https://resources.catalyze.io/paas/getting-started/deploying-your-first-app/domain-names/) contains more detailed information for verifying the key and certificate match as well as information about wildcard certificates and certificate chains.  Please contact Catalyze [support](https://catalyzeio.zendesk.com/hc/en-us/requests/new).   We will establish a secure method to share the files and schedule a time to update the certificate.


## How should my SSL certificate chain be formatted?

Catalyze terminates SSL connections with an Nginx server. If you are downloading SSL certificates
from your provider and have the option to download the Nginx chain, that is a good place to start.
Typically, your SSL cert provider will supply you with a certificate for your site along with a
bundle of their certificates to complete the "chain". These files are combined to create the 
certificate chain. Getting the cert chain ordered correctly can be a little tricky, but fortunately
there are lots of examples to be found. One thing to remember is to include your site's server 
certificate first. Here are a few commands and links to get you started in the right direction.

Concatenate the certificates into a single file, referred to as the cert chain (note, you might
also see these files referred to as PEM files):

```
$ cat www.example.com.crt bundle.crt > www.example.com.chained.crt
```

To verify the bundle or chain matches the certificate use this command:

```
openssl verify -verbose -purpose sslserver -CAfile chain.crt www.example.com.crt
```

Next, before uploading your certificate chain, test it out locally to verify it matches your private key.
See the following question for an overview. After you verify the cert chain upload the entire chain
to the Catalyze Dashboard for your Environment.

Links:

* [Digicert - PEM File Creation](https://www.digicert.com/ssl-support/pem-ssl-creation.htm)
* [GoDaddy - Installing an SSL Cert - Nginx](https://support.godaddy.com/help/article/6722/installing-an-ssl-certificate-nginx?locale=en)
* [Nginx - Certificate Chains](http://nginx.org/en/docs/http/configuring_https_servers.html#chains)


## How can I validate my SSL certificate locally?

Validating your SSL certificate locally just takes a few steps. The main check we want to do is
ensure that the certificate matches the private key. This is an important step because if they do
not match the server will not start up. If you are searching around for more validation steps, note
that Catalyze uses an Nignx server to terminate SSL connections.

To verify your certificate matches the private key, use the following commands. If you do not
already have a chained cert or a pem file see the previous SSL articles about creating that.

```
$ openssl rsa -noout -modulus -in server-private.key | openssl md5
$ openssl x509 -noout -modulus -in server.pem | openssl md5
```

If you want to go a step further you can run Nginx locally with your certs installed. Here's a quick
overview of doing that:

* [Digicert - Install SSL Certs on Nginx](https://www.digicert.com/ssl-certificate-installation-nginx.htm)

