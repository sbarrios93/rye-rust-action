# Rye Installer for Python GitHub Action

![GitHub Workflow Status](https://img.shields.io/github/workflow/status/sbarrios93/rye-rust-action/CI?style=for-the-badge)
![GitHub release (latest by date)](https://img.shields.io/github/v/release/sbarrios93/rye-rust-action?style=for-the-badge)

This GitHub Action allows you to install [Rye Project Manager](https://github.com/mitsuhiko/rye) on your GitHub Actions runner.

## Table of Contents

- [Rye Installer for Python GitHub Action](#rye-installer-for-python-github-action)
  - [Table of Contents](#table-of-contents)
  - [Overview](#overview)
  - [Features](#features)
  - [Usage](#usage)
    - [Inputs](#inputs)
    - [Outputs](#outputs)
    - [Example Workflow](#example-workflow)
  - [License](#license)

## Overview

Rye is a project manager for Python applications that makes it easy to manage dependencies, build, and test projects. This GitHub Action provides an easy way to install Rye on a GitHub Actions runner, allowing you to take advantage of Rye's powerful features in your CI/CD pipelines.

## Features

- Installs Rye on the GitHub Actions runner
- Caches the Rye installation for faster builds
- Supports stable Rust toolchain
- Provides output for the installed Rye commit hash

## Usage

### Inputs

No inputs are required for this action.

### Outputs

| Output Name       | Description                                           |
| ----------------- | ----------------------------------------------------- |
| `rye_commit_hash` | The commit hash of the installed Rye version. |

### Example Workflow

```yaml
name: Python Rye Workflow
on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main

jobs:
  rye-build:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout repository
      uses: actions/checkout@v3

    - name: Install Rye
      uses: sbarrios93/rye-rust-action@v1
      id: rye-installer

    - name: Show Rye version
      run: |
        echo "Installed Rye commit hash: ${{ steps.rye-installer.outputs.rye_commit_hash }}"
        rye --version

    - name: Sync dependencies
      run: |
        rye sync
```

## License

This project is licensed under the [MIT License](LICENSE).
