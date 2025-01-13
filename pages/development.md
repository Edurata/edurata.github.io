---
layout: default
title: Local development
---

# Local development

## Setup of yaml linter in VSCode

To get the yaml linter working in VSCode, you need to install the [YAML extension](https://marketplace.visualstudio.com/items?itemName=redhat.vscode-yaml) and configure the schemas in the settings. The schemas are used to validate the yaml files against a schema. The schemas are publicly available and can be found at the following locations:

- [workflow schema](https://edurata.io/workflow/v1)
- [function schema](https://edurata.io/function/v1)

To configure the schemas in VSCode, you need to add the following to your settings.json, which you can access by pressing `Ctrl+Shift+P` and typing `Preferences: Open Settings (JSON)`:

```json	
  "yaml.schemas": {
    "https://edurata.io/workflow/v1": [
      "*.eduwc.yml",
      "*.eduwc.yaml"
    ],
    "https://edurata.io/function/v1": [
      "*.edufc.yml",
      "*.edufc.yaml"
    ]
  },
```

This will enable the linter for all files with the extensions `.eduwc.yml`, `.eduwc.yaml`, `.edufc.yml` and `.edufc.yaml`.