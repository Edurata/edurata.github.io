---
layout: default
title: Definitions
has_children: true
parent: Registry
nav_order: 1
---

# Definitions

Definitions are defined in yaml inside a git repository in order to configure cloud resources that should be created. There is definition files for workflows and functions.

## General information

Workflows and function definitions contain [meta information](configs#interfacesconfigmd) like name, description, title, which are partly informative for the user and partly used for the platform to identify the definition.

## Additional information

Workflows and function definitions each contain specific information that is different between workflows and functions. For workflows this is for example the `steps` attribute and for function definitions it is `runtime`, `entrypoint` and `include` attributes.

## Interface

It is also possible to define an optional [interface](./interface.md) which defines the validation of input and output values of workflows and functions
