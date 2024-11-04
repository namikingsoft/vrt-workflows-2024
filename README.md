# GitHub Actions workflows for Visual Regression Test

```yml
name: VRT

on:
  pull_request:
    types:
      - opened
      - synchronize
  # for cache
  push:
    branches:
      - main
      - master

jobs:
  vrt:
    uses: org_name/vrt-workflows-2024/.github/workflows/snapshots.yml@main
    with:
      snapshots_command: npm run snapshot
      snapshots_dirpath: test/vrt.e2e.ts-snapshots
    secrets:
      your_repo_github_token: ${{ secrets.GITHUB_TOKEN }}
      vrt_repo_github_token: ${{ secrets.VRT_GITHUB_TOKEN }}
```
