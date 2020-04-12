# azure-pipelines-templates

Azure Pipelines templates for my repos.

**Note**: for my personal use only. I do not guarantee any stability around here. In other words: please don't use this.

## Setup

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
      ref: refs/tags/3.0
```

Then reference templates as `<template>.yml@templates`.

## Jobs

### `job--python-test.yml`

Expected scripts: `scripts/install`, `scripts/test`.

Example:

```yaml
jobs:
  - template: job--python-test.yml@templates
    parameters:
      jobs:
        # Minimal definition:
        py37: null

        # Complete definition:
        py38_dj30_windows_pg:
          coverage: true
          os: windows
          services:
            postgres: pg11
          variables:
            DJANGO_VERSION: "3.0"
```

### `job--python-check.yml`

Expected scripts: `scripts/install`, `scripts/check`.

Example:

```yaml
jobs:
  - template: job--python-check.yml@templates
    parameters:
      pythonVersion: "3.8"
```

## Steps

### `step--python-install.yml`

Expected scripts: `scripts/install`.

Example:

```yaml
steps:
  - template: step--python-install.yml@templates
    parameters:
      pythonVersion: "3.8"
```

### `step--python-test.yml`

Expected scripts: `scripts/install`, `scripts/test`.

Example:

```yaml
steps:
  - template: step--python-test.yml@templates
    parameters:
      pythonVersion: "3.8"
      coverage: true  # optional
```
