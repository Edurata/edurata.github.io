---
layout: default
title: Workflow Definition
parent: Definitions
grand_parent: Registry
nav_order: 2
---

# Workflow config

In order to register a workflow into the registry you need to write a config that defines the workflow fully.

```yaml
apiRevision: edurata.io/workflow/v1
name: foo-workflow
description: |
  Test workflow to show how to define a workflow.
interface: ...
steps:
  step1:
    source:
      # Source by registry
      name: foo-function
      revision: 12
    props:
      dep1: ${inputs.input1} # This is passing the input "input1" to the input dep1 on step1
      dep2: ${variables.var1} # This is passing the variable "var1" to dep2
      dep3: ${secrets.secret1} # This is passing a secret of "secret1" to dep3
  step2:
    source:
      # Source by git
      repoUrl: https://github.com/Edurata/edurata-functions.git
      path: general/example-function
      ref: main
    props:
      dep1: ${step1.output1} # This is passing the output "output1" of step1 to the input dep1 on step2 as defined in the function "example-function"
      dep2: example of interpolation ${step1.output2} ! # This is passing a string with interpolation to dep2 as defined in the function "example-function"
```
