# azure-pipelines-templates

Azure Pipelines templates for my repos.

**Note**: for my personal use only. I do not guarantee to any stability around here. In other words: please don't use this.

## Usage

Add this at the beginning of `azure-pipelines.yml`:

```yaml
resources:
  repositories:
    - repository: templates
      type: github
      name: florimondmanca/azure-pipeline-templates
```

Then reference templates as `<template>.yml@templates`.
