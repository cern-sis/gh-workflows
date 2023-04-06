# Setup docker

## Description

This action install and configure docker in the current job.


## Examples

```yaml
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Code
        uses: actions/checkout@v3
        with:
          ref: ${{ inputs.ref }}

      - name: Setup docker
        uses: cern-sis/gh-workflows/.github/actions/docker-setup@v4.0.0
```
