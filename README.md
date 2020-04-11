# azure-pipelines-templates

Azure Pipelines templates for my repos.

**Note**: for my personal use only. I do not guarantee to any stability around here. In other words: please don't use this.

## Usage

First, add a service connection named `github`:

```
Project settings
  > Service connections
    > New service connection
      > GitHub 
```

Add this at the beginning of `azure-pipelines.yml`:

```yaml
resources:
  repositories:
    - repository: templates
      type: github
      endpoint: github
      name: florimondmanca/azure-pipelines-templates
      ref: refs/tags/0.1
```

Then reference templates as `<template>.yml@templates`.
