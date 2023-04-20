# Shared Workflows for GitHub Actions

This repo contains [GitHub Action Reusable Workflows](https://docs.github.com/en/actions/using-workflows/reusing-workflows) which may be called from other workflows in other repositories. These can be used to better secure your code and CI/CD pipeline.

Click the workflows below to expand for details

## Workflows
<details>
    <summary><h3>CI-Security-Scan</h3></summary>
    <h3>Get Started</h3>
    
To set up the CI security workflow, create a new file, `{repo_root}/.github/workflows/ci-security-scan.yml` and paste in the folowing:

```yaml
name: "CI Security Scan"
on:
    pull_request:
        types: - opened
        branches:
            - master
            - main
            - develop
jobs:
    run-security-scan:
        name: 'Untamed Theory CI Security Scan'
        uses: untamed-theory/shared-workflows/.github/workflows/ci-security-scan.yml@main

```
<br>
<h3>About this workflow</h3>
This workflow automatically scans CI configuration files for known injectable syntax and other known security vulnerabilities and misconfigurations. It leverages the Checkov scanner under the hood.

It will detect and assess:
- GitHub Actions workflow files
- GitLab CI files
- Bitbucket pipelines configurations files

<br>
<h3>Config</h3>

| Parameter | Default| Description
| --- | --- | --- |
| enforce-status-check | false | Will fail a status check for vulnerabilities found
| file-name | 'ci-security-scan-results.sarif' | Name for zip file of scan artifacts

</details>

<details>
    <summary><h3>SAST-Security-Scan</h3></summary>
    <h3>Get Started</h3>
    
To set up this workflow, create a new file, `{repo_root}/.github/workflows/security-scan.yml` and paste in the following:

```yaml
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

<br>
<h3>About this workflow</h3>
This is a quick, holistic scan of the source code in your repo leveraging the [ShiftLeft Scanner](https://github.com/ShiftLeftSecurity/sast-scan). It is capable of blocking Pull Request status checks for vulnerabilities found (Critical and High). Or it can conduct non-blocking scans while still producing an artifact. 

It will automatically assess and run the following (where applicable):
- Static Code Analysis
- Dependency Vulnerability Scans
- Credential Detection Scans
- Infrastructure as Code (IaC) Analysis
- Dockerfile and Kubernetes Analysis

<br>
<h3>Parameters & Config</h3>

| Parameter | Default| Description
| --- | --- | --- |
| enforce-status-check | false | Will fail a status check for vulnerabilities found
| file-name | 'security-scan-artifacts' | Name for zip file of scan artifacts
</details>
