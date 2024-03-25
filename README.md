# Pull from Paragon GitHub Action

This GitHub Action allows you to pull from a Paragon project using the Paragraph CLI.

## Usage
Note: It is suggested to name the runner file as "**paragraph_pull_runner.yml**"

```yaml
name: Pull from Paragon

on: 
  workflow_dispatch:
    inputs:
      projectId:
        type: string
        required: true
        description: 'Paragon project id'

      commitId:
        type: string
        required: true
        description: 'Paragon project commit id'

jobs:
  pull_from_paragon:
    name: Pull from Paragon
    runs-on: ubuntu-latest

    permissions:
      contents: write
      
    steps:
      - uses: actions/checkout@v4
      - id: pull
        uses: useparagon/paragraph-pull@v1
        with:
          projectId: ${{ inputs.projectId }}
          commitId: ${{ inputs.commitId }}
          paragonKey: ${{ secrets.PARAGON_CLI_KEY }}
          paragonZeusUrl: ${{ secrets.ZEUS_URL }}
          paragonDashboardUrl: ${{ secrets.DASHBOARD_URL }}
```

Make sure to replace ${{ secrets.PARAGON_CLI_KEY }}, ${{ secrets.ZEUS_URL }}, and ${{ secrets.DASHBOARD_URL }} with your actual secrets.

## Inputs
- projectId
Required. Paragon project ID.

- commitId
Required. Paragon project commit ID.

## Permissions
This action requires the following permissions:

- contents: Write permission to commit and push the changed files back to the repository.
