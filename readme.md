# [check-github-pages](https://github.com/marketplace/actions/check-github-pages)

[![ci](https://github.com/AlexAegis/check-github-pages/actions/workflows/simple-test.yml/badge.svg)](https://github.com/AlexAegis/check-github-pages/actions/workflows/simple-test.yml)

A github action to make your github pages metadata available in ci

## Use

> For a real-world usecase check the workflows of this repository!

```yaml
name: simple-test

on:
  workflow_dispatch:
  push:
    branches: "**"

jobs:
  check-pages:
    runs-on: ubuntu-latest
    outputs:
      pages_enabled: ${{ steps.check_pages.outputs.is_enabled }}
    steps:
      - name: check if github pages is enabled
        id: check_pages
        uses: AlexAegis/check-github-pages@v1
  print:
    name: print results
    runs-on: ubuntu-latest
    if: needs.check-pages.outputs.is_enabled
    needs: [check-pages]
    steps:
      - name: print package data
        run: |
          echo pages are enabled!
```
