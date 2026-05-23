# qihe-slang-dist

This repository publishes prebuilt `slang` binaries for use by `qihe`.

The goal is simple: instead of asking every `qihe` user to build `slang` locally,
this repository uses GitHub Actions to build specific upstream `slang` versions
and attach the resulting binaries to GitHub Releases. `qihe` can then download
those release assets directly.

## What This Repository Contains

- GitHub Actions workflows for building selected `slang` versions
- GitHub Releases containing prebuilt binaries for Linux, macOS, and Windows

## Current Workflows

- [`.github/workflows/release-v11.0.yml`](./.github/workflows/release-v11.0.yml)
  Builds upstream `slang` tag `v11.0`
- [`.github/workflows/release-f31d20e.yml`](./.github/workflows/release-f31d20e.yml)
  Builds upstream `slang` commit `f31d20e5574773e9ebe46bba95efa395966ce5e9`

Each workflow is manually triggered and publishes a draft GitHub Release with
these assets:

- `slang-linux-x86_64.tar.gz`
- `slang-macos-arm64.tar.gz`
- `slang-windows-x86_64.zip`

## How Release Publishing Works

1. Open the repository on GitHub.
2. Go to `Actions`.
3. Select the workflow for the version you want to build.
4. Click `Run workflow`.
5. Wait for the Linux, macOS, and Windows jobs to finish.
6. Review the generated draft release under `Releases`.

Re-running the same workflow updates the same release tag and overwrites files
with the same names. This makes it easier to iterate while debugging the build.

## Release Naming

This repository uses one workflow per upstream version / commit:

- release by version tag: `release-v11.0.yml`
- release by commit: `release-<short-commit>.yml`

The corresponding GitHub release tag matches the upstream reference being built.

## Notes

- The workflows do not currently perform macOS notarization or Windows code
  signing.

## Upstream Reference

Upstream project:

- [MikePopoloski/slang](https://github.com/MikePopoloski/slang)

Relevant upstream references used when preparing these workflows:

- [Build documentation](https://github.com/MikePopoloski/slang/blob/master/docs/building.dox)
- [Release workflow](https://github.com/MikePopoloski/slang/blob/master/.github/workflows/release.yml)
