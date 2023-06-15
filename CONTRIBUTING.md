# Contributing

## Adding Actions

Copy any action that is similar to what you'd like to add. If you don't know which to pick, try the [kustomize-build](./kustomize-build/).

1. Update your readme file with the required steps.
2. Add a testing workflow (see: [testing guide](#testing))
3. Update the [repo readme](README.md).
4. Send a pull request and wait for reviews from ATIPO team.

## Testing

### Testing workflow

All actions you develop must be tested. Please create a workflow to test the action you just developed in the [.github/workflows](.github/workflows/) folder with the name `test-<action-name>`.

Then create a rule to trigger this workflow every time you make changes to the file and create a PR to the main branch.

For an example testing workflow, please see: [.github/workflows/test-kustomize-build.yml](.github/workflows/test-kustomize-build.yml)

### Testing locally

You can test the workflow above locally with [act](https://github.com/nektos/act).

To install `act` on MacOS:

```bash
brew install --HEAD act
```

Setup required environment variables:

```bash
cp .env.example .env
# Edit .env to add any required environment variables.
```

Then run the test script:

```bash
./test.sh
```
