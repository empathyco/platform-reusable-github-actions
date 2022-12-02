# Reusable github actions

This repository is intended to store all of the reusable github actions workflows so, rather than copying and pasting from one workflow to another, you can make your workflows reusable. Feel free to contribute to this repository by adding your own workflows, or by improving existing ones.

## Adding new workflows

To add new reusable workflows you just need to add them under the `.github/workflows` folder, so they can be used from within any repository.

> **Note**
> This is a **PUBLIC** repository so remember to avoid commiting credentials or secrets to the repository,
> every credential or secret needed inside of the workflow should be passed as an input variable.

### Links

[Reusing workflows (Github docs)](https://docs.github.com/en/actions/using-workflows/reusing-workflows)

[About workflows (Github docs)](https://docs.github.com/en/actions/using-workflows/about-workflows)
