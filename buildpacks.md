---
title: Buildpacks - PaaS FAQ
---

# Buildpacks

### What is a buildpack?

A buildpack is a framework for constructing your application's stack. It is extremely flexible and is intended to operate as an agent to your environment. The buildpack agent will attempt to understand your stack and install any dependencies required by it.

### How does the buildpack work?

Catalyze detects your code type automatically and assigns the proper buildpack accordingly. When you push your code to Catalyze the appropriate buildpack creates an executable slug that includes the dependencies for your environment.

### What buildpacks does Catalyze support?

We support the following buildpacks:

- Ruby
- Node.js
- Clojure
- Python
- Java
- Gradle
- Grails
- Scala
- Play
- PHP (Laravel is only supported in version 5+)

### Can I run my own buildpack?

**Note: third party buildpacks are not fully supported by Catalyze and should be used at the user's own risk.**

It is possible to create your own build pack or use one of the many existing [third party buildpacks](https://devcenter.heroku.com/articles/third-party-buildpacks). To use a custom build pack the BUILDPACK_URL environment variable should be set via the [Catalyze PaaS CLI](https://resources.catalyze.io/paas/cli/sections/vars/) or via the [Catalyze Dashboard](https://resources.catalyze.io/paas/getting-started/deploying-your-first-app/environment-variables/).

```
catalyze vars set BUILDPACK_URL=<BUILDPACK_URL>
```

###Why is Laravel only supported in versions 5+ and above?

Pre-5+ Laravel lacks major functionality required to work behind load-balancers and proxies. This functionality is crucial to running on a PaaS. Laravel 5.1 has LTS support and is currently the only supported version of Laravel on the Catalyze PaaS. This is demonstrated in our [sample PHP/Laravel application](https://github.com/catalyzeio/php-example-app) You can deploy Laravel 4 and below on Catalyze, but it is not supported by Catalyze and you are responsible for managing the intracacies of a distributed Laravel on your own. If you want to read some programmer-lever details about this, read about how `Request::secure()` [requires a hack to work on Laravel 4 behind a proxy](http://laravel-tricks.com/tricks/fix-ssl-in-laravel-4-when-server-is-behind-a-load-balancer-or-a-reverse-proxy).
