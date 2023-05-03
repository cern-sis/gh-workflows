# Build docker image

## Description

This action bundle all the steps needed to build a docker image in your workflow without any previous setup. This action always push the resulting image, tags and cache to the remote registry so credentials are mandatory. This action already installs docker there is no need to use [docker setup](../docker-setup) in the same workflow.


## Inputs

| Name | Required | Type | Description |
| ---- | -------- | ---- | ----------- |
| `image` | Yes | String | The name of the image being built. |
| `context` | No | String | The context used during the build. |
| `tags` | No | String | A list of additional tags [reference](https://github.com/marketplace/actions/docker-metadata-action#tags-input). |
| `registry` | No | String | The regitry used to store the image after the build. |
| `username` | Yes | String | Username to authenticate on the registry. |
| `password` | Yes | String | Password to authenticate on the registry. |
| `stage` | No | String | The [stage](https://docs.docker.com/build/building/multi-stage/) to build . |
| `dockerfile` | No | String | The path to the Dockerfile. |
| `cache` | No | Bool | Enable/disable remote cache. |
| `build-args` | No | String | Additional build arguments. |

## Examples

Build an image with the default tags and push it to docker hub:
```yaml
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Code
        uses: actions/checkout@v3
        with:
          ref: ${{ inputs.ref }}

      - name: Build and push
        uses: cern-sis/gh-workflows/.github/actions/docker-build@v4.0.0
        with:
          image: myorg/mycoolimage
          username: ${{ secrets.DOCKER_USERNAME }}
          password: ${{ secrets.DOCKER_PASSWORD }}
```

Build an image with custom tags and push it to CERN registry:
```yaml
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Code
        uses: actions/checkout@v3
        with:
          ref: ${{ inputs.ref }}

      - name: Build and push
        uses: cern-sis/gh-workflows/.github/actions/docker-build@v4.0.0
        with:
          image: cern-sis/mycoolproject/test
          tags: |
            type=ref,event=branch
            type=ref,event=pr
            type=ref,event=tag
          registry: registry.cern.ch
          username: ${{ secrets.REGISTRY_USERNAME }}
          password: ${{ secrets.REGISTRY_PASSWORD }}
```

Build a specific stage of my Dockerfile in a specific context:
```yaml
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Code
        uses: actions/checkout@v3
        with:
          ref: ${{ inputs.ref }}

      - name: Build and push
        uses: cern-sis/gh-workflows/.github/actions/docker-build@v4.0.0
        with:
          image: myorg/mycoolimage
          contest: ./docker/source
          dockerfile: ./somewhereelse/Dockerfile
          username: ${{ secrets.DOCKER_USERNAME }}
          password: ${{ secrets.DOCKER_PASSWORD }}
```
