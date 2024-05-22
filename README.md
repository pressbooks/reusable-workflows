## Reusable workflows for Pressbooks

This repository contains reusable workflows that can be used on any Pressbooks repository to reduce code duplication and
maintenance across several repos which use similar automation as part of our CI/CD processes. With centralized
workflows, we can update a specific action or workflow in one place and run it everywhere, instead of having to push
identical changes to every repo that uses the action.

### Reusable workflows list

* update-pot.yml

This reusable workflow automatically generates and commits a new .pot file to any PR branches.

This reusable workflow automatically generates and commits machine-readable translation files to any PR branches which
update the .po files in that repository.

* npm-build.yml

This reusable workflow would run the `npm run lint/build --if-exists` command on any PR branches which update the .js
files in that

* prepare-release.yml

This reusable workflow would open Release Candidate PRs and bump versions on required files defined inside (
release-please-config.json) in each repo, this also will tag and release a new version with an artifact attached when
the pull request gets merged.

* auto-merge.yml

This reusable workflow would automatically merge chore translations PRs when the CI checks pass.

* composer-update.yml

This reusable workflow would run the `composer update` when a dependency within a Bedrock repository is updated.

* pb-plugin-tests.yml

This reusable workflow would run the desired test matrix for a plugin repository.

### Restrictions and behaviors for the source repository

Note the following restrictions and behaviors for the source repository and workflow:

* Required workflows can be stored in any repository folder and are not restricted to the .github/workflows folder like
  normal workflows. If a required workflow calls a reusable workflow, the reusable workflow must be stored in the
  .github/workflows folder. When calling a reusable workflow, a required workflow must use the full path and ref to the
  reusable workflow. For example, `{owner}/{repo}/.github/workflows/{filename}@{ref}`.

* If the required workflow is contained in a private repository, you must ensure that workflows within the repository
  are accessible by other repositories in your organization. For more information, see "Allowing access to components in
  a private repository."

* Workflows stored in a public repository can be configured as required workflows for any repository in your
  organization. Workflows stored in a private repository can only be configured as required workflows for other private
  repositories in your organization.

* CodeQL is not supported in required workflows because CodeQL requires configuration at the repository level. For
  information on configuring code scanning, see "Configuring code scanning for a repository."

### Further reading

https://docs.github.com/en/actions/using-workflows/required-workflows

https://docs.github.com/en/actions/using-workflows/reusing-workflows
