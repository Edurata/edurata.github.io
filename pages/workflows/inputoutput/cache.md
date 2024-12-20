---
layout: default
title: Cache
parent: Input Output Processing
grand_parent: Workflows
nav_order: 2
---

## Cache

If you want to cache files between steps you can use the cache. The cache is a local filesystem that is mounted into the container and can be used to store files between steps. The cache is persisted between executions and is available for all executions.

If you set the attribute `cache: true` in the workflow definition, the cache will be mounted into the container at the path which is available in the environment variable `CACHE_MOUNT_DIR` inside the container or under the path of `${meta.cacheMountDir}` inside the workflow definition. You can then use this path to store files in the cache. For example in python:

### Example

Suppose there is a function `function1` used in two steps: a `step1` which saves a file at the path that is provided through the input `fileinput` and a second step `step2` that uses the same function to access the file at the same location. The workflow config is the following:

```yaml
steps:
  step1:
    source:
      name: function1
      revision: 1
    dependencies:
      fileinput: ${meta.cacheMountDir}/${meta.deploymentId}/${meta.executionId}/file.txt
  step2:
    source:
      name: function1
      revision: 1
    dependencies:
      fileinput: ${meta.cacheMountDir}/${meta.deploymentId}/${meta.executionId}/file.txt
```

The function is identical with the [artefacts example](./artefacts.md), the only difference is the types of the inputs are just strings:

_function definition_

```yaml
interface:
  inputs:
    fileinput:
      type: string # ! this one is different !
      description: the filepath were to save the file
```

Now in `step1` you can just create the file at the location that is provided through the input `fileinput` and in `step2` you can access the file at the same location.
