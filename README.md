## Reusable workflows for Pressbooks

This repository contains reusable workflows that can be used on any Pressbooks repository to reduce code duplication and
maintenance across several repos which use similar automation as part of our CI/CD processes. With centralized
workflows, we can update a specific action or workflow in one place and run it everywhere, instead of having to push
identical changes to every repo that uses the action.

### Reusable workflows list

* update-pot.yml

This reusable workflow automatically updates translation files (.pot) whenever relevant files change in a pull request and opens a PR with the changes.

* update-mo.yml

This reusable workflow automatically updates translation files (.mo) whenever relevant .po files change in a pull request and amends the commit with .mo files.

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

* crowdin.yml

This reusable workflow syncs translations with Crowdin. It supports three actions: `upload` (push source POT files), `download` (pull translations, compile MO files, and create a PR), and `seed` (one-time upload of both sources and existing translations to bootstrap a Crowdin project). Supports both open-source and private projects via a `project_type` input. Each repo uses its own Crowdin branch name for isolation.

* stale-issue-handler.yml

This reusable workflow automatically manages stale issues and pull requests. It marks items as stale after 90 days of inactivity (configurable), then closes them 30 days later (configurable). You can exempt specific labels, customize messages, and run in dry-run mode for testing.

* po-dashboard.yml

**Recommended for Product Owners:** Centralized dashboard that monitors multiple repositories from a single location. Combines weekly triage tracking (needs-review items) AND assignment tracking across all repos you oversee. Creates a consolidated dashboard issue and sends single Slack notifications. Perfect when you manage many repos and want one unified view.

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

https://docs.github.com/en/actions/using-workflows/reusing-workflows

## Usage Examples

### Stale Issue Handler

```yaml
name: StaleBot 🔧
on:
  schedule:
    - cron: '0 1 * * *'  # Daily at 1 AM UTC
  workflow_dispatch:  # Manual trigger

jobs:
  stale:
    uses: pressbooks/reusable-workflows/.github/workflows/stale-issue-handler.yml@main
    with:
      stale_days: 90
      close_days: 30
      stale_label: 'stale'
      exempt_labels: 'pinned,security,bug'
      dry_run: false
```

**Configuration Options:**
- `stale_days`: Days before marking stale (default: 90)
- `close_days`: Days after stale before closing (default: 30)
- `stale_label`: Label applied when stale (default: 'stale')
- `exempt_labels`: Comma-separated labels to skip (default: 'pinned,security')
- `only_issues`: Only process issues, skip PRs (default: false)
- `only_prs`: Only process PRs, skip issues (default: false)
- `dry_run`: Test mode without making changes (default: false)
