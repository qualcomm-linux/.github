# Qualcomm Linux GitHub Organization

This repo contains workflow templates and other org level config and files

## Qualcomm Linux Repolinter GitHub Action

Qualcomm Linux repos should enable the Repolinter GitHub Action upon creation. This action runs the Repolinter tool, which lints open source repositories for common issues.

### Initial setup

1. Navigate to the new repo
1. Click on Actions
1. If you have existing actions in the repo, click "New workflow", else skip to next step
1. Scroll to "Workflows created by Qualcomm Innovation Center" and click "Set up this workflow" under "Qualcomm Linux Organization Repolinter Workflow"
1. Click "Start commit" and then "Commit new file" after selecting the appropriate e-mail under "Choose which email address to associate with this commit"
1. This will create a GitHub Action config file in your repo under the path `.github/workflows/qualcomm-linux-organization-repolinter.yml`
1. Adjust it as needed, e.g. the Repolinter action is configured to run on Push and Pull Requests into the main/master branch, but you may want to further adjust when it runs.

### Customizing Repolinter rules

When the GitHub Action is run, it first checks your Qualcomm Linux repo for a local `repolint.json` file at the root directory. If it doesn't find one it'll use the default Qualcomm Linux Repolinter ruleset, which is located here https://github.com/quic/.github/blob/main/repolint.json

To customize the default Qualcomm Linux repolinter ruleset (e.g. to add some language specific file extensions for the license check), copy the `repolint.json` file (from https://github.com/quic/.github/blob/main/repolint.json) and place it at the root of your Qualcomm Linux repo. Now you can edit and tweak it as applicable.

## Preflight Checker Workflow

This workflow utilizes a reusable workflow to run a series of preflight checks on your code. The checks include:
* **[Repolinter](https://github.com/qualcomm-linux/qli-actions)**: Checks the repository for consistency and adherence to coding standards.
* **[Semgrep](https://github.com/qualcomm-linux/qli-actions)**: Runs a static analysis tool to detect potential security vulnerabilities and coding errors.
* **[Copyright-License-Detector](https://github.com/qualcomm/copyright-license-checker-action)**: Checks for proper copyright and licensing information in the code.
* **[PR-Check-Emails](https://github.com/qualcomm/commit-emails-check-action)**: Verifies that the commit emails are properly formatted.

Reusable workflow is available at: [multi-checker-pipeline](https://github.com/qualcomm-linux/qli-actions/.github/workflows/multi-checker.yml)
If you want to disable any checker for example semgrep, you can set `semgrep: false` in the `with` section of the workflow. Default value is `true` for all checkers.
