---
layout: default
title: Triggers
parent: Deployments
nav_order: 1
---

# Triggers

## Scheduled executions

If the executions should run in a regular interval, the `schedule` attribute can be set inside the [workflow definition](../registry/definitions/workflowDefinition.md) to a fitting cron value.

## Manual executions

You can also execute a workflow through a button in the UI or through an api call at `api.edurata.com/deployment/{deploymentId}/execute`
