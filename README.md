# SonarQube Cloud Scanner Action

- The pipeline is designed to run a sonarqube cloud scanner
- The pipeline is designed to be as generic as possible, so they can be easily reused in any project.
- This repository is a part of the generic GitHub Actions pipeline collection that can be used in any project.

## Usage

Here is a basic example of how you can integrate it in your project.

<details>
  <summary>Example workflow</summary>

This workflow is executed automatically on push to the main branch, on a pull request and can also be executed manually from the actions tab `workflow_dispatch`.

In the code below you need to replace `<sonar-token>` with the SonarQube Cloud token you want to use.

```yml
name: Run SonarCloud scanner

on:
  workflow_dispatch:
  pull_request:
  push:
    branches:
      - main

jobs:
    sonarcloud-scanner:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      # Using the action
      - name: Install dependencies
        uses: minvws/action-sonarcube-cloud/.github/actions/sonarcloud@main
        with:
            sonar-token: <sonar-token>
```

</details>

### Configuration

The action has inputs. The inputs are:

- sonar-token: the SonarQube Cloud token
- project-base-dir: set the sonar.projectBaseDir analysis property, default is `.`

## Contributing

If you want to contribute a new pipeline, please check the reusable workflow guidelines in the
[GitHub documentation](https://docs.github.com/en/actions/using-workflows/reusing-workflows#creating-a-reusable-workflow).
