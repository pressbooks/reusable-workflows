## Reusable workflows for Pressbooks

This repository contains reusable workflows that can be used on any Pressbooks repository to reduce code duplication and maintenance across several repos which use similar automation as part of our CI/CD processes. With centralized workflows, we can update a specific action or workflow in one place and run it everywhere, instead of having to push identical changes to every repo that uses the action.

### Workflows list

* lint-build.yml

This workflow is used to lint and build frontend assets. Each time a PR is opened we can ensure that contributions follow our code style guidelines and the build step works as expected.

* ci-check.yml

This workflow checks to see the pull request titles follow the expected conventions used by Pressbooks (conventional commit prefixes)

* update-mo.yml

This reusable workflow automatically generates and commits machine-readable translation files to any PR branches which update the .po files in that repository.

* prepare-release.yml

This reusable workflow would open Release Candidate PRs and bump versions on required files defined inside (release-please-config.json) in each repo, this also will tag and release a new version with an artifact attached when the pull request gets merged.

### How to use a required workflow

1. Create a workflow in this repo
2. Register the required workflow in GitHub (organization settings)
3. Attach the workflow to the repos where it should run (organization settings).
4. Enjoy your new workflow.

### Restrictions and behaviors for the source repository

Note the following restrictions and behaviors for the source repository and workflow:

* Required workflows can be stored in any repository folder and are not restricted to the .github/workflows folder like normal workflows. If a required workflow calls a reusable workflow, the reusable workflow must be stored in the .github/workflows folder. When calling a reusable workflow, a required workflow must use the full path and ref to the reusable workflow. For example, `{owner}/{repo}/.github/workflows/{filename}@{ref}`.

* If the required workflow is contained in a private repository, you must ensure that workflows within the repository are accessible by other repositories in your organization. For more information, see "Allowing access to components in a private repository."

* Workflows stored in a public repository can be configured as required workflows for any repository in your organization. Workflows stored in a private repository can only be configured as required workflows for other private repositories in your organization.

* CodeQL is not supported in required workflows because CodeQL requires configuration at the repository level. For information on configuring code scanning, see "Configuring code scanning for a repository."

### Further reading

https://docs.github.com/en/actions/using-workflows/required-workflows

https://docs.github.com/en/actions/using-workflows/reusing-workflows
