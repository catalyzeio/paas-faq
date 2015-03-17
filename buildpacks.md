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
- PHP

### Can I run my own buildpack?

**Note: third party buildpacks are not fully supported by Catalyze and should be used at the user's own risk.**

It is possible to create your own build pack or use one of the many existing [third party buildpacks](https://devcenter.heroku.com/articles/third-party-buildpacks).