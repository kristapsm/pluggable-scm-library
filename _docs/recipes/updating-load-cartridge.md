---
layout: docs
title: Updating Load_Cartridge job
permalink: /docs/recipes/updating-load-cartridge/
---

This section describes two ways how to update your ADOP Instance to inherit Pluggable SCM -

* **Automatically** - quick way
* **Manually** - more like a workaround

# Automatic way

1. Re-run **Load_Platform** job to grab all the DSL codes for the new **Load_Cartridge** job
2. Update your Jenkins image to be the latest version on the Github repository in your compose and then re-initialise ADOP using **./adop compose init -m _name-of-your-machine_**
  - _Note:_ Just check the latest Jenkins image version [here](https://github.com/Accenture/adop-docker-compose/blob/master/docker-compose.yml#L203), it contains a couple of additional environment variables, plugins and some properties files in the right location. This change has been described below using _Manual_ way.
3. Re-generate your Workspace and Project to ensure you have the latest version of **Load_Cartridge** job which should contain some additional fields