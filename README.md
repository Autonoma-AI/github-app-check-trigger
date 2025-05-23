# Autonoma AI GitHub Action

[![Version](https://img.shields.io/badge/version-v1.0.0-blue)](https://github.com/getautonoma/autonoma-testing-action/releases) [![License](https://img.shields.io/badge/license-MIT-green)](LICENSE)

A GitHub Action to trigger and monitor Autonoma AI’s self-healing UI tests for web and mobile apps right from your CI/CD workflows.

## 🚀 Features

- **Trigger On-Demand** and scheduled test runs in Autonoma AI  
- **Wait & Fail**: optional blocking mode to wait for completion and fail on test failures  
- **Self-Healing**: leverage Autonoma’s AI-driven maintenance—no fragile selectors  
- **CI/CD Integration**: plug into any GitHub Actions pipeline for continuous quality

## 🔧 Inputs

| Input           | Description                                                                                   | Required | Default  |
|-----------------|-----------------------------------------------------------------------------------------------|:--------:|:---------|
| `test-type`     | The type of test to run (`folder` or `test`).                                                 |    no    | `folder` |
| `test-id`       | The ID of the test or folder to run.                                                          |    no    | `""`      |
| `client-id`     | The client ID of an API key generated in Autonoma’s platform (set as a GitHub secret).        |    no    | `""`      |
| `client-secret` | The client secret of an API key generated in Autonoma’s platform (set as a GitHub secret).    |    no    | `""`      |

## 📤 Outputs

| Output   | Description                                                 |
|----------|-------------------------------------------------------------|
| `status` | Status of the Autonoma test call (`success` or `failure`).  |
| `message`| Response message from Autonoma.                             |
| `url`    | URL to view the test run in Autonoma.                       |

## 🛠️ Usage

Add this to your workflow (e.g. `.github/workflows/ui-tests.yml`):

```yaml
name: Autonoma UI Tests

on:
  push:
    branches: [ main ]
  pull_request:

jobs:
  ui-test:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Run Autonoma UI Tests
        uses: getautonoma/autonoma-testing-action@v1
        with:
          api-token: ${{ secrets.AUTONOMA_API_TOKEN }}
          project-id: your-project-id
          test-suite-id: your-test-suite-id
          app-url: https://your-app.example.com
          wait-for-completion: true
          poll-interval-seconds: 30

      - name: Print report URL
        run: echo "View test report at ${{ steps.run-autonoma.outputs.report-url }}"
```
