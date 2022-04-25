# Lighthouse

## Workflow Setup

Name: Lighthouse

Trigger: Workflow Call

## Example Usage

```yaml
lighthouse:
    uses: axelerant/reusable-workflows/.github/workflows/lighthouse.yml@main
    with:
      PROJECT_DIR: path/to/root
      NODE_VERSION: lts/gallium
      NODE_CACHE_TYPE: yarn
      NODE_CACHE_DEP_PATH: path/to/yarn.lock
    secrets:
      BASE_URL: ${{ secrets.CYPRESS_BASE_URL }}
      BASIC_USERNAME: ${{ secrets.CYPRESS_BASIC_USERNAME }}
      BASIC_PASSWORD: ${{ secrets.CYPRESS_BASIC_PASSWORD }}
      LHCI_GITHUB_APP_TOKEN: ${{ secrets.LHCI_GITHUB_APP_TOKEN }}
      LHCI_TOKEN: ${{ secrets.LHCI_TOKEN }}
      LHCI_DASHBOARD_URL: ${{ secrets.LHCI_DASHBOARD_URL }}
      LHCI_BASIC_USERNAME: ${{ secrets.LHCI_BASIC_USERNAME }}
      LHCI_BASIC_PASSWORD: ${{ secrets.LHCI_BASIC_PASSWORD }}
```

## Prerequisites

- Lighthouse CI Server hosted publicly
- Lighthouse CI Server must have authentication setup
- Repo must have Lighthouse CI Github App installed
- Project must have `lighthouserc.js` config file at root directory
- Project must use `yarn`

## Inputs

### PROJECT_DIR

The main directory of the project to serve as root for Lighthouse

### NODE_VERSION

The version of node to use.
Example: `lts/gallium`

### NODE_CACHE_TYPE

The type of cache to use for Node.
Example, `yarn`

### NODE_CACHE_DEP_PATH

The path to the cache file
Example of cache file: `yarn.lock`

## Secrets

### BASE_URL

The URL of the site that we want to run Lighthouse on

### BASIC_USERNAME

The username required for the site. Can be blank if no authentication has been setup.

### BASIC_PASSWORD

The password required for the site. Can be blank if no authentication has been setup.

### LHCI_GITHUB_APP_TOKEN

Token generated for using the Lighthouse Github App
Can be used as LHCI_GITHUB_TOKEN if using the PTA method instead

### LHCI_TOKEN

Build Token generated when running `lhci wizard`

### LHCI_DASHBOARD_URL

The URL of the Lighthouse CI Server

### LHCI_BASIC_USERNAME

Username as setup in Lighthouse CI authentication

### LHCI_BASIC_PASSWORD

Password as setup in Lighthouse CI authentication

## What this workflow does

1. Check out code of current branch
2. Setup Node
3. Run Lighthouse Tests
  a. `cd` into `PROJECT_DIR`
  b. Run `yarn` to install packages/dependencies
  c. Run `lhci autorun` using `lighthouserc.js` config at root directory along with username and password for LHCI server

## Additional Notes

This workflow only runs Lighthouse CI with some basic authentication. The actual tests run and other features can be configured freely in `lighthouserc.js`.


