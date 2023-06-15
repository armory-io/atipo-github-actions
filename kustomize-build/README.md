# Kustomize build action

This action renders a kustomize directory and diff the rendered output with the one in default branch.

## Inputs & Outputs

See [action.yml](action.yaml) for more details.

## Usage

```yaml
- name: Kustomize build and diff
  id: kustomize-diff
  uses: armory-io/atipo-github-actions/kustomize-build@main
  with:
    install_kustomize: true
    kustomize_version: 5.0.3
    kustomize_overlay_paths: "kustomize-build/test/kustomize/dev,kustomize-build/test/kustomize/prod"
    target_ref: ${{ env.DEFAULT_REF }}
    source_ref: ${{ env.PR_REF }}
```

## Scenarios

```yaml
name: Render manifests and diff against default branch

on:
  pull_request:
    branches:
      - main

env:
  PR_REF: ${{ github.event.pull_request.head.ref }} # PR branch
  DEFAULT_REF: ${{ github.event.repository.default_branch }} # Default branch

jobs:
  kustomize:
    name: "Diff kustomize manifests against default branch"
    runs-on: ubuntu-22.04
    steps:
      - uses: actions/checkout@v3
        with:
          ref: ${{ env.PR_REF }}
          fetch-depth: 2 # Otherwise, you will failed to push refs to dest repo

      - name: Kustomize build and diff
        id: kustomize-diff
        uses: armory-io/atipo-github-actions/kustomize-build@main
        with:
          install_kustomize: true
          kustomize_version: 5.0.3
          kustomize_overlay_paths: "deploy/dev,deploy/prod"
          target_ref: ${{ env.DEFAULT_REF }}
          source_ref: ${{ env.PR_REF }}

      - name: "Send PR comment"
        if: ${{ steps.kustomize-diff.outputs.kustomize_diff }}
        uses: mshick/add-pr-comment@v2
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        with:
          message: |
            ${{ steps.kustomize-diff.outputs.kustomize_diff }}

      - uses: stefanzweifel/git-auto-commit-action@v4
        with:
          branch: ${{ env.PR_REF }}
          commit_message: Apply rendered kustomize build
```
