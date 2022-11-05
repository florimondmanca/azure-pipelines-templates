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
      ref: refs/tags/6.0
```

Then reference templates as `<template>.yml@templates`.

## Jobs

### `job--python-test.yml`

Expected scripts: `make install-python`, `make test`.

Example:

```yaml
jobs:
  - template: job--python-test.yml@templates
    parameters:
      jobs:
        # Minimal definition:
        py311: null

        # Complete definition:
        py311_dj30_windows_pg:
          coverage: true
          os: windows
          services:
            postgres: pg11
          variables:
            DJANGO_VERSION: "3.0"
```

### `job--python-check.yml`

Expected scripts: `make install-python`, `make check`.

Example:

```yaml
jobs:
  - template: job--python-check.yml@templates
    parameters:
      pythonVersion: "3.11"
```

### `job--python-docs-build.yml`

Build docs under a Python environment.

Expected scripts: `make install-python`, `make docs`.

Example:

```yaml
jobs:
  - template: job--python-docs-build.yml@templates
    parameters:
      pythonVersion: "3.11"
```

### `job--python-publish.yml`

Publish a Python package to PyPI.

#### Assumptions

- `make install-python`, `make build`, `make publish` must exist.
- `twine` and `wheel` must be installed.
- `token` refers to a [PyPI API token](https://pypi.org/help/#apitoken) set via a [Python upload service connection](https://docs.microsoft.com/en-us/azure/devops/pipelines/library/service-endpoints?view=azure-devops&tabs=yaml#python-package-download-service-connection) (Project settings > Service connection > New... > Python package upload). It may be provided through a variable group (Library > Variable group...), as shown below.

#### Example

_This example assumes you want to publish on tags._

```yaml
trigger:
  - master
  - refs/tags/*

variables:
  # ...
  - group: pypi-credentials  # Sets $(pypiToken)

stages:
  - stage: test
    jobs: # ...
  - stage: publish
    condition: startsWith(variables['Build.SourceBranch'], 'refs/tags/')
    jobs:
      - template: job--python-publish--tag.yml@templates
        parameters:
          token: $(pypiToken)
          pythonVersion: "3.11"
```

## Steps

### `step--python-provision.yml`

Setup a Python runtime and a cache for pip dependencies.

Example:

```yaml
variables:
  PIP_CACHE_DIR: $(Pipeline.Workspace)/.cache/pip

steps:
  - template: step--python-provision.yml@templates
    parameters:
      pythonVersion: "3.11"
```

### `step--python-install.yml`

Expected scripts: `make install-python`.

Example:

```yaml
variables:
  PIP_CACHE_DIR: $(Pipeline.Workspace)/.cache/pip

steps:
  - template: step--python-install.yml@templates
    parameters:
      pythonVersion: "3.11"
```

### `step--python-test.yml`

Expected scripts: `make install-python`, `make test`.

Example:

```yaml
steps:
  - template: step--python-test.yml@templates
    parameters:
      pythonVersion: "3.11"
      coverage: true # optional
```

### `step--node-provision.yml`

Expected scripts: `make install-node`.

Setup a Node.js runtime and a cache for NPM dependencies.

Example:

```yaml
variables:
  NODE_CACHE_FOLDER: $(Build.SourcesDirectory)/node_modules

steps:
  - template: step--node-provision.yml@templates
    parameters:
      nodeVersion: "18.x"
```

### `step--node-install.yml`

Expected scripts: `make install-node`.

Setup a Node.js runtime, a cache for NPM dependencies, and install NPM dependencies.

Example:

```yaml
variables:
  NODE_CACHE_FOLDER: $(Build.SourcesDirectory)/node_modules

steps:
  - template: step--node-install.yml@templates
    parameters:
      nodeVersion: "18.x"
```
