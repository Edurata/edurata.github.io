---
layout: default
title: Executions
parent: Deployments
nav_order: 2
---

# Executions

An "execution" is more closely defined as an either scheduled or manually triggered attempt to run all [functions](../functions/index.md) and nested functions inside the [workflow](../workflows/index.md) of a [deployment](index.md).

# Inputs variables

Inputs into an execution of a deployment can occur in several ways. They are resolved in the following order, overriding the ones before:

- Variables set in the [execution](index.md) itself. For example when triggering through the webhook or through the API.
- Variables set in the [deployment](index.md)
- Explicit inputs set in the [workflow](../workflows/index.md)
- The defaults set in the [workflow](../workflows/index.md)
- Explicit inputs set in the [function](../functions/index.md)