# SonarQube Scanner GitHub Action

This repository provides a reusable GitHub Action for running SonarQube scans in GitHub Workflows.
It is designed to standardize the logic around the original [SonarQube Scanner Action](https://github.com/SonarSource/sonarqube-scan-action),
automatically handling details such as providing the correct branch name for pull requests and checking if the pull request is a fork.

## Features

- Standardizes the [SonarQube Scanner Action](https://github.com/SonarSource/sonarqube-scan-action) for consistent usage across projects
- Ability to configure the project base directory for SonarQube analysis
- Provide branch name to the scan action when running on pull requests
- Prevents the scan action from running on pull requests from forks by default

## Usage

Here is a basic example of how you can integrate it in your project.

<details>
  <summary>Example workflow</summary>

This workflow is executed automatically on push to the main branch, on a pull request and can also be executed manually from the actions tab `workflow_dispatch`.

In the code below you need to replace `${{ secrets.SONAR_TOKEN }}` with the secret that contains the SonarQube token you want to use.

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
        uses: minvws/action-sonarcube-cloud@v1
        with:
            sonar-token: ${{ secrets.SONAR_TOKEN }}
```

</details>

### Configuration

The action has inputs. The inputs are:

- sonar-token: the SonarQube token
- project-base-dir: set the sonar.projectBaseDir analysis property, default is `.`
- allow-run-on-fork: allow SonarQube scan to run on pull requests from forks (default: false)

## Contribution

If you plan to make non-trivial changes, we recommend to open an issue beforehand where we can discuss your planned changes.
This increases the chance that we might be able to use your contribution (or it avoids doing work if there are reasons why we wouldn't be able to use it).

Git commits must be signed. Please check the [Signing commits documentation on GitHub](https://docs.github.com/en/github/authenticating-to-github/signing-commits).

## License

This repository is released under the EUPL 1.2 license. [See LICENSE](LICENSE.txt) for details.

## Part of iCore

This package is part of the iCore project.
