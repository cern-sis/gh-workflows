# Kubernetes project update

## Description

This action can be used to notify the `cern-sis/kubernetes` repository that your project has been updated and new docker images are available. This will trigger updates and deployments depending on the environments impacted.


## Inputs

| Name | Required | Type | Description |
| ---- | -------- | ---- | ----------- |
| `images` | Yes | String | The list of new images available. |
| `token` | Yes | String | The Personal Access Token used to send the event. |

## Examples

```yaml
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: send event
        uses: cern-sis/gh-workflows/.github/actions/kubernetes-project-update@v4.0.0
        with:
          images: |
            "registry.cern.ch/cern-sis/mycoolproject/mytestimage:v1"
            "myorg/myotherproject@sha256:xxzxzxzxz"
          token: ${{ secrets.PAT }}
```
```yaml
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: send event
        uses: cern-sis/gh-workflows/.github/actions/kubernetes-project-update@v4.0.0
        with:
          images: "myorg/myotherproject@sha256:xxzxzxzxz"
          token: ${{ secrets.PAT }}
```
