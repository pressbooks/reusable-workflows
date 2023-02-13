## Reusable/Required workflows for Pressbooks

This repository contains reusable workflows that can used on any Pressbooks repository to reduce code duplication on our automation efforts.

The most outstanding benefit of required workflows is that we don't need to push any code change in our repos anymore, we can build standarized steps in one place.

### Workflows list

* lint-build.yml

This workflow is used to lint and build frontend assets, this way everytime a PR is opened we ensure the contributions follows our code style guidelines and the js build still works.


### How to use a required workflow

1. Create a workflow in this repo
2. Register the required workflow in Github (organization settings)
3. Attach the workflow to the repos where it should run (organization settings).
4. Enjoy your new workflow.

### Restrictions and behaviors for the source repository

Note the following restrictions and behaviors for the source repository and workflow:

* Required workflows can be stored in any repository folder and are not restricted to the .github/workflows folder like normal workflows. If a required workflow calls a reusable workflow, the reusable workflow must be stored in the .github/workflows folder. When calling a reusable workflow, a required workflow must use the full path and ref to the reusable workflow. For example, `{owner}/{repo}/.github/workflows/{filename}@{ref}`.

* If the required workflow is contained in a private repository, you must ensure that workflows within the repository are accessible by other repositories in your organization. For more information, see "Allowing access to components in a private repository."

* Workflows stored in a public repository can be configured as required workflows for any repository in your organization. Workflows stored in a private repository can only be configured as required workflows for other private repositories in your organization.

* CodeQL is not supported in required workflows because CodeQL requires configuration at the repository level. For information on configuring code scanning, see "Configuring code scanning for a repository."

### Further read

https://docs.github.com/en/actions/using-workflows/required-workflows

https://docs.github.com/en/actions/using-workflows/reusing-workflows