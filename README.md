# Reusable IaC Workflows

## About

This repository contains reusable workflows to be used to create and manage resources on AWS using Terraform.

## How to use

You must create a workflow file in your own repository and you may call the reusable workflow.
You will be able to choice your action strategy and the branches to be triggered.

### Dependencies

- Github Repository
- Self hosted runner group (with IAM roles atached)

### Configuration

Create the file **.github/wotkflows/myplanworkflow** and call the reusable workflows as below:

```yaml
name: Testing - Reusable Workflow

on:
  push:
    branches:
      - 'branch name'
jobs:
  call-reusable-workflow:    
    uses: stack-spot/stackspot-workflows/.github/workflows/reusable_workflow.yaml@5c5e0e05729332f624c396dd221c5fba2e685693
    with:
      runner_group: runner-group-name
      working_directory: terraform/
      github_event_name: ${{ github.event_name }}
      tag: $GITHUB_RUN_NUMBER
    secrets:
      AWS_ACCOUNT_ID: ${{ secrets.AWS_ACCOUNT_ID_SANDBOX }}
      AWS_REGION: ${{ secrets.AWS_REGION_SANDBOX }}
      GIT_PIPE_TOKEN: ${{ secrets.GIT_PIPE_TOKEN }}
      INFRACOST_API_KEY: ${{ secrets.INFRACOST_API_KEY }}

```

### Parameters

|parameter          |description                                     |
|-------------------|------------------------------------------------|
| runner_group      | The name of the Self hosted Runner group       |
| working_directory | The path of your terraform files               |
| AWS_ACCOUNT_ID    | The identifier of the AWS account              |
| AWS_REGION        | The region where the resources will be applied |
| GIT_PIPE_TOKEN    | Github token for the workflow                  |
| INFRACOST_API_KEY | The API Key of the Infracost which will be used|

## Support

Stacks Environment Team
