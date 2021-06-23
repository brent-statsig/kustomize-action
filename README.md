# kustomize-action [![ts](https://github.com/int128/kustomize-action/actions/workflows/ts.yaml/badge.svg)](https://github.com/int128/kustomize-action/actions/workflows/ts.yaml)

This is an action to run `kustomize build` in parallel.


## Getting Started

To run this action:

```yaml
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: int128/kustomize-action@v1
        id: kustomize
        with:
          pattern: overlays/*/kustomization.yaml
      - run: find ${{ steps.kustomize.outputs.directory }}
```

### Outcome

For example, when the pattern matches to the following files:

```
overlays/development/kustomization.yaml
overlays/production/kustomization.yaml
```

This action generates the following files:

```
/tmp/somewhere/overlays/development/generated.yaml
/tmp/somewhere/overlays/production/generated.yaml
```

You can get the base directory `/tmp/somewhere` from `outputs.directory`.


## Inputs

| Name | Required | Description
|------|----------|------------
| `pattern` | yes | glob patterns to `kustomization.yaml`
| `base-directory` | no | base directory to compute a relative path to `kustomization.yaml` (default to workspace)
| `max-process` | no | max number of kustomize processes (default to 5)


## Outputs

| Name | Description
|------|------------
| `directory` | directory to results of `kustomize build`
