# GitHub Actions Reusable Workflows

[![License](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/license/MIT)

This repository is a collection of reusable workflows to be used in many github actions pipelines.

### Description

Each workflow consists of a series of steps that aims to install and run a specific tool, like gitleaks for example, which scans any repo to find passwords, apis keys or credentials that may be hard coded into the application code.  

### Usage

To use a specifc workflow in a pipeline, it must be called in the yaml pipeline file that will build and deploy the application. 

<strong>Example:</strong>
```yaml
name: Terraform pipeline

on:
  workflow_dispatch:
  push:
    branches: [ main ]

jobs:
  scan:
    uses: guilherme-aroliveira/gh-workflows/.github/workflows/gitleaks.yaml@main
```

In some pipelines will be necessary to define settings like the working directory to be used or even the terraform version to be used. And apart from these configurations it will be also necessary some secrets like the aws role created that allows github actions to provision services on the aws account.

<strong >Example:</strong>
```yaml
plan:
  uses: guilherme-aroliveira/gh-workflows/.github/workflows/tf-plan.yaml@main
  with:
    tf_version: '1.12.2'
  secrets:
     AWS_ASSUME_ROLE: ${{ secrets.AWS_ASSUME_ROLE }}
```

### Tools Used 

- GitHub Actions
- YAML
- Bash

## License

Copyright (c) 2026, Guilherme Oliveira. All rights reserved.

Licensed under the MIT License. See [LICENSE](LICENSE)