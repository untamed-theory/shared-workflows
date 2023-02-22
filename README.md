# Untamed Theory - Shared Workflows for GitHub Actions

This repo contains [GitHub Action Reusable Workflows](https://docs.github.com/en/actions/using-workflows/reusing-workflows) which may be called from other workflows in other repositories. These can be used to better secure your code and CI/CD pipeline.

## Workflows

- `security-scan`

## `security-scan`
This is a quick, holistic scan of the source code in your repo leveraging the [ShiftLeft Scanner](https://github.com/ShiftLeftSecurity/sast-scan). It is capable of blocking Pull Request status checks for vulnerabilities found (Critical and High). Or it can conduct non-blocking scans while still producing an artifact. 

| Parameter | Default| Description
| --- | --- | --- |
| enforce-status-check | false | Will fail a status check for vulnerabilities found
| file-name | 'security-scan-artifacts' | Name for zip file of scan artifacts

It will automatically assess and run the following (where applicable):
- Static Code Analysis
- Dependency Vulnerability Scans
- Credential Detection Scans
- Infrastructure as Code (IaC) Analysis
- Dockerfile and Kubernetes Analysis

To set up this workflow, create a new file, `{repo_root}/.github/workflows/security-scan.yml` and paste in the following:

```
name: "My Security Scan"
on:
    pull_request:
        types: - opened
        branches:
            - master
            - main
            - develop
jobs:
    run-security-scan:
        name: 'Untamed Theory Security Scan'
        uses: untamed-theory/shared-workflows/.github/workflows/security-scan.yml@main
```