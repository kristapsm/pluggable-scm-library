---
layout: docs
title: What is Pluggable SCM Library
permalink: /docs/recipes/what-is-it/
---

In brief, Pluggable SCM allows user to use his own desired SCM provider, currently _BitBucket_ and _Gerrit_ are supported.

By enabling a standard interface, Java reflection can be used to return dynamic groovy closures in cartridge which would act the same as default DSL methods depending on the SCM provider.

There are two parts of ADOP that are affected by using this library:

* [Load_Cartridge job](todo:url)
* [Cartridge DSL code](https://kristapsm.github.io/adop-cartridges-cookbook/docs/recipes/adding-a-pluggable-scm/)

The _pluggable.scm_ package contains:

* _SCMProvider_ - an interface which defines the specification of an SCM provider
* _SCMProviderDataStore_ - an interface for SCM provider data store specification
* _SCMProviderFactory_ - an interface for SCM provider factory definition responsible for parsing the providers properties and instantiating the correct SCM provider
* _SCMProviderHandler_ - a class responsible for dispatching SCM provider requests to the correct SCM provider factory
* _SCMProviderInfo_ - annotation to mark SCM providers

More specific information can be found in [Javadocs](https://kristapsm.github.io/pluggable-scm-library/groovydocs/)
