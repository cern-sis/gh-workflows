# Kubernetes project new images

## Description

This action can be used to notify the `cern-sis/kubernetes` repository that your project has been updated and new docker images are available.

## Inputs

| Name | Required | Type | Description |
| ---- | -------- | ---- | ----------- |
| `event-type` | Yes | String | The type of the event triggering this action. `release` or `update`. |
| `images` | Yes | String | The list of new images available. |
| `token` | Yes | String | The Personal Access Token used to send the event. |

## Examples

```yaml
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: send event
        uses: cern-sis/gh-workflows/.github/actions/kubernetes-project-update@v5.0.0
        with:
          event-type: update
          images: |
            registry.cern.ch/cern-sis/mycoolproject/mytestimage:v1
            myorg/myotherproject@sha256:xxzxzxzxz
          token: ${{ secrets.PAT }}
```
```yaml
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: send event
        uses: cern-sis/gh-workflows/.github/actions/kubernetes-project-update@v5.0.0
        with:
          event-type: release
          images: myorg/myotherproject@sha256:xxzxzxzxz
          token: ${{ secrets.PAT }}
```

## Know issues

When using a multiline string (`|` symbol in YAML), don't surround your images with double quotes `"`.

