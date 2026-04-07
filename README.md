<!--
SPDX-FileCopyrightText: Copyright (C) 2025 Chen Linxuan <me@black-desk.cn>

SPDX-License-Identifier: MIT
-->

# clean-action

[![checks][badge-shields-io-checks]][actions]

[badge-shields-io-checks]: https://img.shields.io/github/check-runs/black-desk/clean-action/master
[actions]: https://github.com/black-desk/clean-action/actions

A GitHub Action for running [clean](https://github.com/black-desk/clean) to lint text files for common whitespace and line ending issues.

## Usage

Create a file at `.github/workflows/lint.yml` in your repository:

```yaml
name: Lint Text Files

on:
  push:
    paths:
      - '**/*'
  pull_request:
    paths:
      - '**/*'

jobs:
  lint:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Lint with clean
        uses: black-desk/clean-action@master
        with:
          # Optional: pass arguments to clean
          extra_args: '--ignore "*.md" --ignore "target/*"'
```

## Inputs

- `extra_args` (optional): Arguments passed as a single string to the clean binary, e.g. `--ignore "*.md" --ignore "target/*"`.

## Outputs

- `json`: JSON output from the clean tool.
- `yaml`: YAML output from the clean tool.

## Behavior

- The action runs clean with both `--json` and `--yaml` and writes the results to `${{ steps.<id>.outputs.json }}` and `${{ steps.<id>.outputs.yaml }}`.
- The results are also appended to the GitHub Actions Step Summary.
- You can reference these outputs in subsequent workflow steps.

## License

This project follows [the REUSE Specification](https://reuse.software/spec-3.3/).

You can use [reuse-tool](https://github.com/fsfe/reuse-tool) to generate an SPDX Document of all files in the project like this:

```bash
reuse spdx
```
