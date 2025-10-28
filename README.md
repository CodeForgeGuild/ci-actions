# ci-actions

### Reusable GitHub Workflows

This repository contains callable GitHub Actions workflows that can be reused across multiple repositories in the organization.
The goal is to centralize and standardize CI/CD processes, making them easier to maintain and evolve.

#### Available Workflows

**1. Release Workflow**

Creates and manages **GitHub releases** with support for **movable tags**.
It automates version tagging and release creation, ensuring consistent release management across repositories.

```yml

name: CI Release Version

on:
  pull_request:
    types: [closed]
    branches: [main]

permissions:
  contents: write
  pull-requests: read

jobs:
  release:
    if: github.event.pull_request.merged == true
    uses: CodeForgeGuild/ci-actions/.github/workflows/release.yml@v0
    secrets:
      GH_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

**2. Trivy Scan Workflow**

Runs a **Trivy vulnerability scan** on the codebase or container image and decorates the **pull request** with the scan results.
Useful for automated security checks during development.

```yml

name: CI Trivy Scan

on:
  pull_request:
    types: [opened, synchronize, reopened]
    branches: [main]

permissions:
  contents: read
  pull-requests: write

jobs:
  trivy:
    name: Trivy Scan
    uses: CodeForgeGuild/ci-actions/.github/workflows/trivy-scan.yml@v0

```

**Features**:

- Runs Trivy to detect vulnerabilities.
- Adds scan summary as a PR comment.
- Can be integrated into any repository with minimal setup.



