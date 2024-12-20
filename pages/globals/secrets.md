---
layout: default
title: Secrets
parent: Globals
nav_order: 2
---


# Secrets

## Usage for runtime configuration

If you want to use environment variables that should be passed to certain workflows you can store them globally in the globals section.

## Usage for private external registries

You can target private repositories (such as a private image repository or private git repository) as a source in your workflow definition.

In order for this to work, you first need to specify a secret with the name of either the `imageRepoUrl` or `repoUrl` the corresponding secret type and value a valid token that should be sent as authentication header with any request.

## Usage for oauth tokens

Some apis require oauth tokens to authenticate. You can authenticate through a few selected oauth providers by creating a secret with the desired scope of the token and then connecting it. If you then specify the secret in the workflow definition it will be on each usage passed to the function or workflow. The token is also automatically refreshed if it is expired.