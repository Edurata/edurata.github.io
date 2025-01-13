---
layout: default
title: Function Sources
parent: Sources
grand_parent: Registry
nav_order: 1
---

# Function sources

## Direct

## Git

Git source is practical if you are still in development and need to do fast updates.

- **repoUrl**: The repository url of the function
- **path**: The path inside the repository to the folder containing `.edufc.yml`
- **ref**: The branch, or commit hash that you want to target. Defaults to the default branch

{: .info }
If the deployment detects changes (there is a newer git commit than the deployed one) it will automatically create a new function version in the registry. If a previous version with the same `ref` is present it will automatically select that one.

{: .info }
The name for the function will either be taken from `.edufc.yml` if specified or fall back to a combination of repoUrl, path and ref of the source.

{: .warning }
If you use a default branch or tag as `ref` to target a function and push another commit to it, the changes will not be deployed automatically. In this case you need to additionally retrigger the deployment.

### Example

The following workflow configs in which functions are defined as sources in steps

```yaml
apiRevision: edurata.io/workflow/v1
name: test-workflow
steps:
    foo-step:
        ...
        source:
            repoUrl: https://github.com/Edurata/edurata-functions
            path: crud/axios
            ref: main # alternatively leave this field empty to target the default branch
    next-step:
        ...
        source:
            repoUrl: https://github.com/Edurata/edurata-functions
            path: crud/axios
            ref: b6284c0 # this targets a direct commit ref
```

### Private Git repositories

If you need to target a private repository you need to create a [Secret](../../globals/secrets.md) with the `repoUrl` as name, type as repository and value as access token.

## Image Repo

You can target an image repo as source if you want to run a whole image instead of just code.

- **imageRepoUrl**: The repository Url
- **tag**: The tag of the image Repo

### Example

```yaml
apiRevision: edurata.io/workflow/v1
name: test-workflow
steps:
    foo-step:
        ...
        source:
            imageRepoUrl: docker/whalesay
            tag: latest # alternatively leave this field empty to target the latest branch
```
