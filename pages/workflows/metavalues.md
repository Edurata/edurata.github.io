---
layout: default
title: Meta Values
parent: Workflows
nav_order: 1
---

# Meta Values

The following meta values are available for use in the [workflow definition](../registry/definitions/workflowDefinition.md) with the same syntax as dependencies:

- `${meta.executionToken}`: The token generated for this execution to authenticate with the platform. You can use it to make selected api calls.
- `${meta.workflowId}`: The id of the workflow.
- `${meta.apiUrl}`: The url of the edurata api. (https://api.edurata.com/v1)
- `${meta.deploymentId}`: The deploymentId. Useful for scoping files in the cache.
- `${meta.executionId}`: The executionId. Useful for scoping files in the cache.
- `${meta.workflowId}`: The workflowId. Useful for scoping files in the cache.
- `${meta.cacheMountDir}`: The directory where the cache is mounted.
