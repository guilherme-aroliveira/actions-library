# GitHub Actions Reusable Workflows

[![License](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/license/MIT)

This repository is a collection of reusable workflows to be used in many github actions pipelines.

### Description

Each workflow consists of a series of steps that aims to install and run a specific tool, like gitleaks for example, which scans any repo to find passwords, apis keys or credentials that may be hard coded into the application code.  

### Usage

To use a specifc workflow in a pipeline, the workflow must be called in the yaml pipeline file that will build and deploy the application. 

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

In some pipelines it will be necessary to define settings like the working directory to be used or even the terraform version to be used. And apart from these configurations it will be also necessary to define some secrets like the aws role created that allows github actions to deploy services on the aws account.

<strong >Example:</strong>
```yaml
plan:
  uses: guilherme-aroliveira/gh-workflows/.github/workflows/tf-plan.yaml@main
  with:
    tf_version: '1.12.2'
  secrets:
     AWS_ASSUME_ROLE: ${{ secrets.AWS_ASSUME_ROLE }}
```

>Note: Each workflow uses a set of secrets and inputs that makes them more agnostic, but in order to use them it's important create each secret with the <strong>same name</strong> in the github repo that will use the pipeline that will call these workflows.

***

### Roadmap

This is still a work in progress, I might make some changes in these workflows or add new ones. 

There are many way to create the steps in a github actions workflow, but I decided to avoid using standard actions as much as possible, and the reason for this is that we don't know what code these actions may use. 

So I prefer to use in each step, some basic shell scripts which makes easier to debug and also to understand what each workflow is doing.

### Tools Used 

- GitHub Actions
- YAML
- Bash

### License

Copyright (c) 2026, Guilherme Oliveira. All rights reserved.

Licensed under the MIT License. See [LICENSE](LICENSE)