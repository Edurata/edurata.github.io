---
layout: default
title: Registry
has_children: true
nav_order: 5
---

# Registry

The registry tracks information about your

{: .warning}
There is no "public" searchable registry like npm as of now and is also not planned for security concerns. If you want to reuuse logic of publicly available code you can just point to that git repo in the workflow source block or copy it over to your own repository.

## Config files / Definitions

Both Functions and Workflows are defined through config files. These config files are written in `yaml` and should ideally be hosted in a git repository ([Github](https://github.com/), [Gitlab](https://gitlab.com/), [Bitbucket](https://bitbucket.org/)).

Config files always have a basic structure like the following:

```yaml
apiVersion: "@edurata.io/workflow/v1"
title: Example Function or Workflow
description: Anything to explain what's going on
interface:
  inputs: ...
  outputs: ...
  ...
```

- The _apiVersion_ field defines which schema to use for this config file, defaults to the latest.
- The _interface_ is used to define what information and in which type is allowed to enter or leave Functions or Workflows.
- The _steps_ field only exists in Workflows. It describes the order of how to execute functions

{: .info }
Any of these config files can also be configured through the [User Interface](https://docs.edurata.com/pages/workflows.html) which also provides intelligent lookups and validation.
