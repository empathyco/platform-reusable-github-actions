# Kubernetes diff with Helm

## Workflow explanation

This workflow is intendeed to run in the source repository of any service/application which is deployed in a Kubernetes cluster using Helm. Adding this workflow to your repository will allow you to check the differences between the current version of your application running in the cluster and the changes you are performing in the PR. 

This check is an extra layer of security to ensure that the changes you are performing in the PR are the ones you want to apply to the cluster and your repository is the source of truth of your cluster following the GitOps philosophy.

Also if you are using ArgoCD, this workflow is removing the "noise" created by ArgoCD as it is adding some labels to the resources that are not present in the repository using the mutating admission webhook, so this labels are not shown in the diff.

## Input variables

**runner:** The runner used to run the workflow. It is recommended to use a self-hosted runner.

**folder:** Path to the helm chart of the application.

**release-name:** Name of the release of the application.

**cluster:** Name of the cluster where the application is deployed.

**namespace:** Namespace where the application is deployed.

## Additional notes

To include this workflow in your repository, here you can find a snippet of the code you need to add to your GitHub Actions workflow file:

```yaml
name: K8s resources diff

on:
  pull_request:
    branches:
    - main
    paths:
    - 'applications/**'

jobs:
  # JOB to run change detection
  changes:
    runs-on: [self-hosted]
    # Required permissions
    permissions:
      pull-requests: read
    # Set job outputs to values from filter step
    outputs:
      beacon: ${{ steps.filter.outputs.beacon }}
    steps:
    # For pull requests it's not necessary to checkout the code
    - uses: dorny/paths-filter@v2
      id: filter
      with:
        filters: |
          beacon:
            - 'applications/ether/beacon-service/**'
  beacon:
    needs: changes
    if: ${{ needs.changes.outputs.beacon == 'true' }}
    uses: empathyco/platform-reusable-github-actions/.github/workflows/k8s-diff.yml@main
    with:
      folder: 'applications/ether'
      release-name: 'beacon-service'
      cluster: 'test'
      namespace: 'ether'
    secrets:
      GH_TOKEN: ${{ secrets.SUPPORT_TOKEN }}
      KUBECONFIG: ${{ secrets.KUBE_CONFIG_TEST }}
```