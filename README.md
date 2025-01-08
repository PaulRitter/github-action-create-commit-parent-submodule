# GitHub Action: Creates a Commit when Submodule is Updated (Based on an [this action](https://github.com/releasehub-com/github-action-create-pr-parent-submodule))

**Beware: this will update ALL submodules in the parent repository. I haven't had the motivation to figure out a way to only update the origin repository, due to that not being necessary for my workflow. I am accepting PR's tho.**

This GitHub action creates a new commit against the parent repository when the submodule is updated.

**The end goal of this tool:** Automatically update the submodule in the parent repository.

## How to use

To use this **GitHub** Action you will need to complete the following in the submodule repository:

1. Parent repository has `.gitmodules` configured
2. Store GitHub token into secrets with permissions to write to parent repository
3. Create a new file in your repository called `.github/workflows/submodule-update.yml`
4. Copy the example workflow from below into that new file and modify as needed
5. Commit that file to a new branch
6. Observe the action working

This file should have the following code:

```yml
---
name: Submodule Updates

on:
  push

jobs:
  build:
    name: Submodule update
    runs-on: ubuntu-latest
    steps:
      - name: run action
        id: run_action
        uses: PaulRitter/github-action-create-commit-parent-submodule@v2.0
        with:
          github_token: ${{ secrets.GH_ACTIONS_TOKEN }}
          parent_repository: org/example-repository
          parent_branch: main
```
