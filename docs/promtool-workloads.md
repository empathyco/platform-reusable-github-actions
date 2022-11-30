# Promtool-workloads

## Workflow explanation

This workflow is ONLY intendeed to run in the platform-eks-<env>-workloads repositories.
This workflow is composed of two jobs: 1. **Changed-files:** Gets a list of all folders with changes inside the `/applications` path. 2. **Matrix-job:** Creates as many jobs as folders listed in the first job. Each new job,
get all of the prometheus rules available in the chart of the application and then,
executes the promtool checks to detect possible failures in the prometheus rules.

**Workflow succesful:** All prometheus rules are OK.

**Workflow failure:** One or more prometheus rules are have errors in their syntax.

## Input variables

**Working-directory:** Path in were the applications are deployed.

## Additional notes

If your service/application creates multiple prometheus rules files (other than `prometheus-rules.yaml`),
you may need to add those new files to the reusable workflow,
in order to get all rules properly checked.

You can add as many files as you want to check to the reusable workflow [here](https://github.com/empathyco/platform-reusable-github-actions/blob/main/.github/workflows/promtool-workloads.yml#L65-L72).
