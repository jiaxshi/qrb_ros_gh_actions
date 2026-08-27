
# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [0.2.0] - 2026-08-27

### Added
- Add `upload-artifact` composite action for uploading build artifacts to S3 with configurable retention tagging, supporting both `x86_64` and `aarch64` architectures.
- Add S3 artifact upload support to `ubuntu-build` workflow, including Debian package generation.
- Add `lyrical` ROS distro support to `ubuntu-build` workflow with parameterized runner and container selection.
- Add `env_setup_commands` input to `ubuntu-build` workflow, replacing the previous `apt-packages` input for more flexible environment setup.
- Add `runner` input to `ubuntu-build` workflow, supporting both GitHub-hosted (string) and self-hosted (JSON array) runners with auto-detection from `ros-distro`.
- Add `qcom-preflight-checks` as a reusable workflow, enabling other repositories to call Qualcomm preflight security and compliance checks.
- Add test workflow for `upload-artifact` composite action covering GitHub-hosted runners and lyrical container.

### Changed
- Replace external upload action with in-repo `upload-artifact` composite action in `ubuntu-build`.
- Upgrade `qcom-preflight-checks` dependency to `v2.0.7`.
- Upgrade `actions/checkout` to `v6` across reusable workflows.
- Move workflow inputs to environment variables to fix template injection warnings.
- Configure `ubuntu-build` to use full repo ref when calling `upload-artifact` action.

### Fixed
- Replace `pull_request_target` with `pull_request` across workflows to address security requirements.
- Fix `upload-artifact` to use environment variable check instead of `sts:GetCallerIdentity` for AWS credential detection.
- Fix `upload-artifact` to restore execute permissions after `python3` zipfile extraction.
- Fix `ubuntu-build` to allow artifact upload to continue on error.
- Fix `ubuntu-build` to write AWS credentials to `GITHUB_ENV` before upload step.
- Fix `qcom-preflight-checks` to restore missing `permissions` block.
- Fix manifest name pattern for `qirp-sdk-build-checker`.
- Fix unzip dependency and upgrade `actions/checkout` to `v6` in reusable workflows.

## [0.1.0] - 2025-9-1
### Added
- Add reusable linters for QRB ROS organization. Linter list:  

| Linters              | Description                                            |
| -------------------- | ------------------------------------------------------ |
| `action-lint`        | Lints C++ code using a specified style guide |
| `commit-lint`        | Lints Python code using a specified style guide |
| `cpp-code-style-checker` | Lints C++ code style using cpplint |
| `qirp-sdk-build-checker` | Checks the build results of the QIRP SDK |
| `ubuntu-build`       | Checks the build results of the ROS build on Ubuntu | |
- Add description and usage to each linter actions.