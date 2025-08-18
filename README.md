# SonarQube Scanner GitHub Action

This repository provides a reusable GitHub Action for running SonarQube scans in GitHub Workflows.
It wraps the official [SonarQube Scanner Action](https://github.com/SonarSource/sonarqube-scan-action) to standardize details such as providing the correct branch name for pull requests and checking if the pull request is made from a fork.

## Usage

To use the action, add it to a workflow in your repository:

```yml
name: Run SonarQube scanner

on:
  workflow_dispatch:
  pull_request:
  push:
    branches:
      - main

jobs:
  sonarqube-scanner:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v5

      - name: Run SonarQube scan
        uses: minvws/action-sonarqube@v1
        with:
          sonar-token: ${{ secrets.SONAR_TOKEN }}
```

Make sure to add the `SONAR_TOKEN` secret to your repository's configuration. See [Using secrets in GitHub Actions](https://docs.github.com/en/actions/how-tos/write-workflows/choose-what-workflows-do/use-secrets).

In this basic example, the workflow is executed automatically on push to the `main` branch and on any pull request. And thanks to the `workflow_dispatch` trigger it can also be executed manually from the repository's Actions tab.

### Configuration

The action has the following inputs:

- `sonar-token` (**required**): The SonarQube token.
- `project-base-dir` (optional): Set the `sonar.projectBaseDir` analysis property. Default is `.`.
- `allow-run-on-fork` (optional): Allow SonarQube scan to run on pull requests from forks. Default is `false`.
- `allow-run-on-dependabot` (optional): Allow SonarQube scan to run on pull requests created by Dependabot. Default is `false`.

## Contribution

If you plan to make non-trivial changes, we recommend to open an issue beforehand where we can discuss your planned changes.
This increases the chance that we might be able to use your contribution (or it avoids doing work if there are reasons why we wouldn't be able to use it).

Git commits must be signed. Please check the [Signing commits documentation on GitHub](https://docs.github.com/en/github/authenticating-to-github/signing-commits).

## License

This repository is released under the EUPL 1.2 license. [See LICENSE.txt](./LICENSE.txt) for details.

## Part of iCore

This package is part of the iCore project.
