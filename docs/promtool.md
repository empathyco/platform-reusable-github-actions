# Promtool

## Workflow explanation

This workflow is intendeed to run in the source repository of any service/application.
It is composed of one main job which get all of the prometheus rules of your service helm chart
and perform the promtool test to check whether the rules are OK or not.

**Workflow succesful:** All prometheus rules are OK.

**Workflow failure:** One or more prometheus rules are have errors in their syntax.

## Input variables

**working-directory:** Path to the helm chart of the application.

**prometheus-rules:** Command needed to generate the prometheus rules of your service.

## Additional notes

No additional notes.
