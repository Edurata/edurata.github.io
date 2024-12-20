---
layout: default
title: Steps and Dependencies
parent: Workflows
nav_order: 1
---

# Steps

Steps are the main building block of workflows. They are defined on a flat level in the [workflow definition](../registry/definitions/workflowDefinition.md). The actual order of execution - whether they run in sequence or in parallel - is then automatically inferred based on dependencies in the definition file.

# Dependencies

Dependencies are defined in the [workflow definition](../registry/definitions/workflowDefinition.md) and are used to pass data between steps. Dependencies are defined in the `props` attribute of a step and are resolved by the platform before the step is executed. Dependencies are also important for the platform to determine the order of execution of the steps.

Dependencies are declared using the `${}` syntax. The platform will resolve the value inside the curly braces before the step is executed. The value can be an input, a variable, a secret, or the output of another step. You can use selected (jsonpath syntax)[https://en.wikipedia.org/wiki/JSONPath] to access deeply nested values.:


## Basic Syntax

- `${inputs.input1}`: This is passing the input "input1"
- `${variables.var1}`: This is passing the variable "var1"
- `${secrets.secret1}`: This is passing the secret secret1
- `${step1.output1}`: This is passing the output "output1" of step1
- `foo bar text ${step1.output2}`: This is passing a string with interpolation with a value from step1
- `${meta.executionToken}`: This is passing a meta value, in this case the execution token
- `${inputs.deepObject.foo.bar[0].hallo}`: This is passing a deeply nested value from an input. Will fail if the value is not found or the path is invalid. This syntax is valid for inputs, variables, secrets and steps.
- `${secrets.deepSecret.foo.bar[0].hallo?}`: This is passing a deeply nested value from a secret and will not fail if the value is not found or the path is invalid.

## Foreach syntax

- `${step1[*].test}`: Assuming that step1 is a foreach loop. This will pass the value of the attribute "test" of each iteration of the loop. The same is possible at any depth of the object e.g. `${step1.foo.bar[*].hallo}` if bar is an array.
<!-- - ${step1.foo.bar[?(@.name == 'test')].hallo}`: This will pass the value of the attribute "hallo" of the object in the array bar where the attribute "name" is equal to "test". This is using the jsonpath syntax. -->
- `${step1.otherArray[each.index].test}`: If the current step is a foreach loop it will pass the value of the attribute "test" of the object in the array otherArray at the index of the current iteration. This is useful if you want to iterate over multiple arrays in parallel.

{: .warning }
The `${}` syntax is only available in the `props` attribute of a step. It is specifically not available in the code block of a step. In order to pass data to a function, you need to specify a dependency in the `props` attribute of a step.


## Example with more context

```yaml
steps:
  step1:
    source:
      name: foo-function
      revision: 12
    props:
      dep1: ${inputs.input1} # This is passing the input "input1" to the input dep1 on step1
      dep2: ${variables.var1} # This is passing the variable "var1" to dep2
      dep3: ${secrets.secret1} # This is passing a secret of "secret1" to dep3
```