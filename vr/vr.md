# VR

## Workflow Setup

Name: VR

Trigger: Workflow Call

## Example Usage

```yaml
vr:
    uses: axelerant/reusable-workflows/.github/workflows/vr.yml@main
    with:
      NODE_VERSION: lts/gallium
      NODE_CACHE_TYPE: yarn
      NODE_CACHE_DEP_PATH: path/to/yarn.lock
      PROJECT_DIR: path/to/root
    secrets:
      PERCY_TOKEN: ${{ secrets.PERCY_TOKEN }}
      CYPRESS_BASE_URL: ${{ secrets.CYPRESS_BASE_URL }}
      CYPRESS_BASIC_USERNAME: ${{ secrets.CYPRESS_BASIC_USERNAME }}
      CYPRESS_BASIC_PASSWORD: ${{ secrets.CYPRESS_BASIC_PASSWORD }}
```

## Prerequisites

- Percy must be setup and configured for this project
- Cypress must be setup in this project
- `package.json` must run Percy commands under `vr:drupal`. Check [**Additional Notes**](/vr/vr#additional-notes) for more details.

## Inputs

### NODE_VERSION

The version of node to use.
Example: `lts/gallium`

### NODE_CACHE_TYPE

The type of cache to use for Node.
Example, `yarn`

### NODE_CACHE_DEP_PATH

The path to the cache file
Example of cache file: `yarn.lock`

### PROJECT_DIR

The main directory of the project to serve as root for Lighthouse

## Secrets

### PERCY_TOKEN

The token generated when setting up Percy

### CYPRESS_BASE_URL

The URL you want to run Cypress tests on

### CYPRESS_BASIC_USERNAME

The username used for Cypress

### CYPRESS_BASIC_PASSWORD

The password used for Cypress


## What this workflow does

1. Check out code of current branch
2. Setup Node
3. Run Visual Regression task
  a. `cd` into `PROJECT_DIR`
  b. Run `yarn` to install packages/dependencies
  c. Run `vr:drupal` task setup in `package.json`

## Additional Notes

This workflow runs a task called `vr:drupal` specified in `package.json`.

`vr:dupal` runs `percy exec -- cypress run`


