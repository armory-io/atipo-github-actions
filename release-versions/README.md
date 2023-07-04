# Kustomize build action

This actions use gh-cli to list all the release versions of a repo.

## Inputs & Outputs

See [action.yml](action.yaml) for more details.

## Usage

```yaml
- name: Get all stable release versions
  id: stable-versions
  uses: armory-io/atipo-github-actions/release-versions@main
  env:
    GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
  with:
    target_repo: "hashicorp/terraform"
    from_version: "0.12.0"
    exclude_prereleases: true
    exclude_rc: true
```
