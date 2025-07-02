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
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
      - name: Set version
        id: vars
        run: |
          echo "node_version=$(cat .node-version)" >> $GITHUB_OUTPUT
          echo "playwright_version=$(cat package-lock.json | grep -m1 -E 'playwright.*"[0-9]+\.[0-9]+\.[0-9]+"' | sed -E 's|.*([0-9]+\.[0-9]+\.[0-9]+).*|\1|')" >> $GITHUB_OUTPUT
      - name: Run visual regression test
        uses: namikingsoft/vrt-workflows-2024@main
        with:
          node_version: ${{ steps.vars.outputs.node_version }}
          playwright_image_tag: v${{ steps.vars.outputs.playwright_version }}
          snapshots_command: npm run snapshot --
          snapshots_dirpath: test/vrt.e2e.ts-snapshots
          shard_count: 2
          force_update_base_snapshots: false
          vrt_repo: namikingsoft/vrt-workflows-2024
          your_repo_github_token: ${{ secrets.GITHUB_TOKEN }}
          vrt_github_app_id: ${{ secrets.VRT_GITHUB_APP_ID }}
          vrt_github_app_private_key: ${{ secrets.VRT_GITHUB_APP_PRIVATE_KEY }}
```
