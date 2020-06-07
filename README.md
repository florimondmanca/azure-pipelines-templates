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
      ref: refs/tags/3.1
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

### `job--python-publish.yml`

Publish a Python package to PyPI.

#### Assumptions

- `scripts/install`, `scripts/build`, `scripts/publish`.
- `twine` and `wheel` must be installed.
- `pypiRemote` refers to a [Twine upload service connection](https://docs.microsoft.com/en-us/azure/devops/pipelines/library/service-endpoints#sep-python-upload). The endpoint name and service connection name must be identical.

#### Example

_This example assumes you want to publish on tags._

```yaml
trigger:
  - master
  - refs/tags/*

stages:
  - stage: test
    jobs: # ...
  - stage: publish
    condition: startsWith(variables['Build.SourceBranch'], 'refs/tags/')
    jobs:
      - template: job--python-publish--tag.yml@templates
        parameters:
          pypiRemote: pypi-public
```

## Steps

### `step--python-provision.yml`

Setup a Python runtime and a cache for pip dependencies.

Example:

```yaml
steps:
  - template: step--python-provision.yml@templates
    parameters:
      pythonVersion: "3.8"
```

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
      coverage: true # optional
```

### `step--yarn-provision.yml`

Setup a Node.js runtime and a cache for Yarn dependencies.

Example:

```yaml
steps:
  - template: step--yarn-provision.yml@templates
    parameters:
      nodeVersion: "12.x"
```
