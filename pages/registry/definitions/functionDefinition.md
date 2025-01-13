---
layout: default
title: Function Definition
parent: Definitions
grand_parent: Registry
nav_order: 1
---

# Function config

Function configs contain basically contain the default attributes plus attributes that are necessary for defining the function (runtime, entrypoint).

Take for example the following function defined [here](https://github.com/Edurata/edurata-functions/tree/b6284c0f34f51062591d18c5ba1bfb19f72f8906/crud/axios)

```yaml
apiRevision: edurata.io/workflow/v1
name: axios
description: |
  Generic function to call apis using axios.
runtime: nodejs18
entrypoint: dist/tsc/index.js
include:
  - dist/tsc/**
interface: ...
```

You can see how the interface definition [here](./interface.md)
