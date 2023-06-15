# Atipo Github Actions

This repository stores [GitHub Actions](https://github.com/features/actions) for Armory-ATIPO team's projects, which can be used to do a variety of CI tasks.

## Getting started

Usage information for individual commands can be found in their respective directories.

## List of actions

1. [kustomize-build](./kustomize-build/) - Renders your kustomize manifests and diff the rendered output.
2. ...

## Releases and tags

We can use tags, branches, or SHAs to manage the version of actions within this repository. However, because we have chosen to store more than one action in the same repo, managing versions with tags can be challenging. Using branches, on the other hand, can lead to issues when breaking changes occur.

Therefore, we have chosen to use SHAs as the primary management mechanism for our actions. You can reference our actions by using the following format: `armory-io/atipo-github-actions/<action-name>@sha123...`

## Development

For development details, see the [contributing guide](./CONTRIBUTING.md).
