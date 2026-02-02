# Dependency Review

Dependency review helps you understand dependency changes and the security implications of these changes at every pull request with:
- Which dependencies were added, removed, or updated.
- Which projects use these components.
- Which Vulnerability data are for these dependencies.

Dependency review allows you to "shift left." You can use the provided predictive information to catch vulnerable dependencies before they hit production. 
By checking the dependency reviews in a pull request and changing any dependencies that are flagged as vulnerable, you can avoid vulnerabilities being added to your project.

## How do I setup a dependency review?

You can setup a `dependency-review-action` on any public repository or a private repository, if you have GHAS enabled, by following these steps:

1. Go to the repository's main page.
2. Select the **Actions** tab.
    - If you're already using GitHub Actions, select **New workflow**.
3. Enter _dependency review_ in the search field.
4. Select **Configure** for the **Dependency Review** workflow.
5. Commit the default `dependency-review.yml` file in the repository's `.github/workflows` directory.

<img width="1145" height="589" alt="image" src="https://github.com/user-attachments/assets/61a5b908-c01b-45c9-9da3-ae952fb1f02b" />

The following is an example Dependency Review Action workflow YAML file:

```yaml
# Dependency Review Action Default/Example Workflow
#
# This Action will scan dependency manifest files that change as part of a Pull Request,
# surfacing known-vulnerable versions of the packages declared or updated in the PR.
# Once installed, if the workflow run is marked as required, PRs introducing known-vulnerable
# packages will be blocked from merging.
#
# Source repository: https://github.com/actions/dependency-review-action
# Public documentation: https://docs.github.com/en/code-security/supply-chain-security/understanding-your-software-supply-chain/about-dependency-review#dependency-review-enforcement
name: 'Dependency review'
on:
  pull_request:
    branches: [ "main" ]

# If using a dependency submission action in this workflow this permission will need to be set to:
#
# permissions:
#   contents: write
#
# https://docs.github.com/en/enterprise-cloud@latest/code-security/supply-chain-security/understanding-your-software-supply-chain/using-the-dependency-submission-api
permissions:
  contents: read
  # Write permissions for pull-requests are required for using the `comment-summary-in-pr` option, comment out if you aren't using this option
  pull-requests: write

jobs:
  dependency-review:
    runs-on: ubuntu-latest
    steps:
      - name: 'Checkout repository'
        uses: actions/checkout@v4
      - name: 'Dependency Review'
        uses: actions/dependency-review-action@v4
        # Commonly enabled options, see https://github.com/actions/dependency-review-action#configuration-options for all available options.
        with:
          comment-summary-in-pr: always
        #   fail-on-severity: moderate
        #   deny-licenses: GPL-1.0-or-later, LGPL-2.0-or-later
        #   retry-on-snapshot-warnings: true
```

## How can I configure a dependency review workflow?

There are two methods of configuring the `dependency-review-action` workflow file:
- Inlining the configuration options in your workflow file.
- Referencing a configuration file in your workflow file.

### Inline configuration

If you wanted to configure license checks and custom severity thresholds to control risk from dependency changes, you can configure the `dependency-review-action` workflow file directly as follows:

```yaml
- name: Dependency Review
        uses: actions/dependency-review-action@v4
        with:
          comment-summary-in-pr: always

          # Possible values: "critical", "high", "moderate", "low"
          fail-on-severity: high

          # # ([String]). Block the pull request on these licenses (optional)
          # Possible values: Any SPDX-compliant license identifiers or expressions from https://spdx.org/licenses/
          deny-licenses: GPL-1.0-or-later, LGPL-2.0-or-later
```

### Reference file

The alternative approach is to use a separate configuration file and then reference it in the `dependency-review-action` workflow file.
You can do this as follows:

_NOTE: These examples use a short version number for the action (v4) instead of a server release number like v4.0.0. This guaranteees that the most recent minor version of the action is in use._

1. Create a YAML configuration file (Ex. `dependency-review-config.yml`) in the repository. 
An example of a dependency review configuration file might look like:

```yaml
# Possible values: "critical", "high", "moderate", "low"
  fail-on-severity: moderate

  # You can only include one of these two options: `allow-licenses` and `deny-licenses`
  # ([String]). Only allow these licenses (optional)
  # Possible values: Any SPDX-compliant license identifiers or expressions from https://spdx.org/licenses/
  allow-licenses:
    - GPL-3.0-only
    - BSD-3-Clause
    - MIT
```

2. Reference the configuration file in the `dependency-review-action` workflow file.

```yaml
- name: Dependency Review
      uses: actions/dependency-review-action@v4
      with:
       # ([String]). Representing a path to a configuration file local to the repository or in an external repository.
       # Possible values: An absolute path to a local file or an external file.
       config-file: './.github/dependency-review-config.yml'

       # Syntax for an external file: OWNER/REPOSITORY/PATH/FILENAME@BRANCH
       config-file: 'github/octorepo/.github/dependency-review-config.yml@main'
```

A few considerations to have in mind before implementing dependency review:
- The `allow-licenses` and `deny-licenses` options are mutually exclusive; an error is raised if you use both in the same workflow.
- If the license for a dependency can't be detected, the `dependency-review-action` will inform you, but the action won't fail.
- Some configuration options aren't supported with GitHub Enterprise Server.
- All configuration options are optional.

If you'd like an in-depth look at dependency review configuration options, you can find out more at: https://github.com/marketplace/actions/dependency-review#configuration-options

## How do I enforce dependency review for a repository?

You can use branch-protection rules and the `dependency-review-action` in your repository to enforce dependency reviews on your pull requests. 
By default, the `dependency-review-action` check fails if it discovers any vulnerable packages. 
A failed check blocks a pull request from being merged when the repository owner requires the dependency review check to pass. 
This proactive guardrail ensures insecure dependencies aren't unknowingly introduced into your project.

Here's how to set up a new branch protection rule to enforce dependency review:

1. Go to your repository and select the **Settings** tab.
2. Select **Branches** under **Code and automation** in the left-side menu.
3. Select **Add branch protection rule**. 
    - If you already have branch-protection rules in place, edit the relevant rule to enforce dependency review.
4. Enter a **Branch name pattern**; for example, `main`.
5. Select the **Require a pull request before merging** option.
6. Select the **Require status checks to pass before merging** option.
7. Select the **Require branches to be up to date before merging** option.
8. Enter _dependency-review_ in the search bar.
9. Select `dependency-review` in the search results to add it to the **Status check that is required** list.
10. Select **Create**.

<img width="792" height="765" alt="image" src="https://github.com/user-attachments/assets/561f1ae9-cb4b-4677-812f-4fcc6bd1cce5" />

