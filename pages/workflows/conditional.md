---
layout: default
title: Conditionals
parent: Workflows
nav_order: 1
---

# Conditionals

Conditionals are a way to conditionally run steps in a workflow. They are defined in the [workflow definition](../registry/definitions/workflowDefinition.md) and can be used to skip steps based on the result of a previous step.

## Syntax

You can define the `if` attribute with an object that is evaluated via limited [json logic](https://jsonlogic.com/operations.html) rules.

### The following operators are supported:

- `===`: Strict equality
- `!==`: Strict inequality
- `>`: Greater than
- `<`: Less than
- `>=`: Greater than or equal
- `<=`: Less than or equal
- `and`: Logical AND
- `or`: Logical OR
- `!`: Logical NOT

### The following operators are not supported:

- `var`: Access a variable. Use `${}` syntax instead.
- `if`: Json logic nested statement. Only the top level `if` is supported and uses a single string.
- `log`: Log a message. Is not supported.

## Examples

For a simple equality of the output of a previous step and a string `test`: 
```yaml
"if":
    "===":
        - "${stepId.outputId}",
        - "test"
```	

For a more complex example with multiple conditions and calculation:
```yaml
"if":
    "and":
        - "===":
            - "${stepId.outputId}",
            - "test"
        - ">":
            - "${stepId2.outputId}",
            - "+":
                - 1
                - "${stepId3.outputId}"
```

Checking for existance of a variable:
```yaml
"if":
    "!!": "${variables.var1}",
```

or:

```yaml
"if":
    "!==": 
        - "${variables.var1}"
        - null
```

## If inside a foreach loop

You can also use the `if` attribute inside a foreach loop. In this case the `if` attribute is evaluated for each iteration of the loop. If the condition is met the step is executed, otherwise it is skipped. 

### Examples

Skipping the loop for the first 6 iterations:
```yaml
steps:
  step1:
    foreach: "${inputs.inputArray}"
    props:
      dep1: ${each}
    if:
      ">":
        - "${each.index}"
        - 6
```

Skipping the loop for all iterations where the value is not equal to `test`:
```yaml
steps:
  step1:
    foreach: "${inputs.inputArray}"
    props:
      dep1: ${each}
      dep2: ${inputs.anotherArray[each.index]} # accessing the value of another array at the same index 
    if:
      "===":
        - "${each}"
        - "test"
```