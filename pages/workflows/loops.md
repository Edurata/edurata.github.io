---
layout: default
title: Foreach loops
parent: Workflows
nav_order: 1
---

# Foreach loops

Instead of passing an array as props to a step in a workflow, you can use a foreach loop to iterate over the array and run the step for each element in the array.

## Basic Syntax

Use the reserved `each` keyword to access the current item in the array.

```yaml
steps:
  step1:
    foreach: "${inputs.inputArray}"
    source:
      name: foo-function
      revision: 12
    props:
      arrayItem: ${each}
```

In this example, the step `step1` is executed for each element in the array `inputArray`. The current element is accessed using `${each}`.

## Accessing other arrays

You can also access other arrays in the same step using the `each.index` keyword.

```yaml
steps:
  step1:
    foreach: "${inputs.inputArray}"
    source:
      name: foo-function
      revision: 12
    props:
      arrayItem: ${each}
      otherArrayItem: ${inputs.anotherArray[each.index]}
```

In this example, the step `step1` is executed for each element in the array `inputArray`. The current element is accessed using `${each}`. The value of prop `otherArrayItem` is accessed at the same index using `${inputs.anotherArray[each.index]}`.