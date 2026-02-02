# Dependabot Alerts

If your project relies on external dependencies, you can use valuable resources trying to monitor them. This monitoring process is important, because you have to be aware of changes or vulnerabilities in the code. 
It can also be challenging, because this code isn't a part of your project. 
GitHub helps to automate this process by monitoring your dependencies and then sending Dependabot alerts when it detects a vulnerable dependency your repository uses.

Dependabot alerts are generated for vulnerable dependencies when:
- A new advisory is added to the GitHub Advisory Database.
- The dependency graph for a repository changes.

It's important to keep your manifest and lock files up to date. If the dependency graph doesn't accurately reflect your current dependencies and versions, you could miss alerts for insecure dependencies that you use. 
You might also get alerts for dependencies that you no longer use.

GitHub also reviews pull request attempts to merge changes into the default branch that contain dependency changes. 
A Dependabot alert is generated if this change would introduce a vulnerability. 
This proactive mechanism allows a maintainer to spot and deal with vulnerable dependencies before, rather than after, they reach the main codebase.

<img width="1273" height="541" alt="image" src="https://github.com/user-attachments/assets/2e176e0e-27d3-40ec-bc19-425f64f03493" />

## How do I enable Dependabot alerts?

Dependabot alerts aren't enabled for public or private repositories by default. 
Repository administrators and owners can enable Dependabot alerts for public repositories, private repositories, and for some GitHub Enterprise Server repositories. 
Enabling these features grants GitHub permission to perform read-only analysis of those specific repositories.

### Repositories

To enable Dependabot alerts for public and private repositories, you need to enable both the dependency graph and Dependabot alerts. Follow these steps for each feature:

1. Sign in to your GitHub account and select your profile photo from the upper right.
2. Select **Settings**, then select **Code security and analysis** under **Security** in the left-side menu.
3. Select **Enable all** to the right of the feature you want to enable.
4. If you'd like these settings to be applied to all new repositories, then select the **Automatically enable for new repositories** checkbox.
5. Select **Enable FEATURE** to enable the feature for all the repositories you own.

### Organizations

If you're an organization owner, then you can enable the dependency graph and Dependabot alerts for all repositories in your organization at once:

1. Sign in to your GitHub account and select your profile photo from the upper-right.
2. Select **Your organizations**.
3. Go to **Settings** for the organization in which you'd like to enable Dependabot alerts.
4. Select **Code security and analysis** under **Security** in the left-side menu.
5. Select **Enable all** to the right of the feature you want to enable.
6. If you'd like these settings to be applied to all new repositories in your organization, select the **Automatically enable for new repositories** checkbox.
7. Select **Enable FEATURE** to enable the feature for all the repositories in your organization.

### Enterprise

If you're an enterprise owner, you can enable or disable Dependabot alerts for all current and future repositories that organizations in your enterprise own. 
Your changes affect all repositories.

1. Sign in to your GitHub account and select your profile photo from the upper-right.
2. Go to **Settings** for the enterprise in which you'd like to enable Dependabot alerts.
3. Select **Code security and analysis** under Security in the left-side menu.
4. Select **Enable all** to the right of the feature you want to enable.
5. If you'd like these settings to be applied to all new repositories owned by organizations in your enterprise, select the **Automatically enable for new repositories** checkbox.
6. Select **Enable FEATURE** to enable the feature for all the repositories that organizations in your enterprise own.

## How do I grant access to Dependabot alerts?

Dependabot alerts for a repository are available to people with write, maintain, or admin access to the repository. 
Also, if the repository is part of an organization, Dependabot alerts are available to the organization owners. 

Administrators and owners can also grant other teams and users with access to the repository, permissions to view and dismiss Dependabot alerts by following these steps:

1. Go to the repository's main page.
2. Select **Settings**, then select **Code security and analysis** under **Security** in the left-side menu.
3. In the **Access to alerts** section, type the name of the person or team that you'd like to be able to manage Dependabot alerts in the search bar. Make your selection.
4. Select **Save changes**.

## How do I resolve Dependabot alerts?

The following steps explain how to resolve Dependabot alerts:

1. Go to the repository's main page.
2. Select the repository's **Security** tab.
3. Select **Dependabot** under **Vulnerability alerts** in the left-side menu. A list of the Dependabot alerts for the repository displays.
4. Select the alert you'd like to view.
5. Review the alert details. In some cases, the alert might contain a pull request with an automated security update.
6. Resolve the alert by taking one of the following actions:
  - Review and merge the pull request.
  - Select **Create Dependabot** security update to manually fix the vulnerability.
  - Select the **Dismiss alert** drop-down and choose a reason for dismissing the vulnerability.

## What if my repository doesn't have security updates enabled by default? How do I manually enable security updates?

If the **Automatically enable for new repositories** option for Dependabot security updates is enabled, GitHub automatically enables Dependabot security updates for every new repository that meets the following prerequisites:
- The repository isn't a fork.
- The repository isn't archived.
- The repository is public, or it's private and you've enabled the read-only analysis by the dependency graph and vulnerability alerts in the repository's settings.
- Dependabot security updates aren't disabled for the repository.

If your repository doesn't meet the aforementioned prerequisites, you can manually enable Dependabot security updates as follows:

NOTE: Ensure the dependency graph and Dependabot alerts options are set to Enabled.

1. Sign in to your GitHub account and select your profile photo from the upper-right.
2. Select **Settings**, then select **Code security and analysis** under **Security** in the left-side menu.
3. Select **Enable all** for Dependabot security updates.
4. If you'd like these settings to be applied to all new repositories, select the **Automatically enable for new repositories** checkbox.
5. Select **Enable Dependabot security updates** to enable the feature for all the repositories you own.

### Individual repositories
1. Go to the repository's main page.
2. Select **Settings**, then select **Code security and analysis** under **Security** in the left-side menu.
3. Select **Enable** for Dependabot security updates.

## How do I enable grouped security updates?

To reduce the number of pull requests from security updates, there's a grouped security updates setting you can enable to group sets of dependencies together.
With this option enabled, Dependabot opens a single pull request to update as many vulnerable dependencies as possible for each package ecosystem to secure versions at the same time.

NOTE: In order to use grouped security updates, you need to enable the following features:
- Dependency graph
- Dependabot alerts
- Dependabot security updates

To enable grouped security updates, follow these steps:

### Individual repositories
1. Go to the repository's main page.
2. Select **Settings**, then select **Code security and analysis** under **Security** in the left-side menu.
3. Select **Enable** for **Grouped security updates**.

### Organizations
1. Sign in to your GitHub account and select your profile photo from the upper-right.
2. Select **Your organizations**
3. Select **Settings** next to the organization for which you'd like to enable Dependabot alerts.
4. Select **Code security and analysis** from the left sidebar.
5. Select **Enable all** for **Grouped security updates**.
6. If you'd like these settings to be applied to all new repositories in your organization, select the **Enable by default for new repositories** checkbox.
7. Select **Enable grouped security updates** to enable the feature for all the repositories in your organization.

## How do I enable version updates?

Version updates are another Dependabot feature that helps to manage your dependencies by automatically generating a pull request whenever there's a new version of a package or application that your project depends on.

Users with write permissions can enable Dependabot version updates for a repository by checking a dependabot.yml file into the .github directory of the repository.

The dependabot.yml file should include the following information:

- ```version```: Should be set to 2.
- ```registries```: Optional if you have dependencies in a private registry. This section contains authentication details.
- ```updates```: Include an entry for each dependency you want Dependabot to monitor.

For each package manager, include:
- ```package-ecosystem```: Specifies the package manager.
- ```directory```: Specifies the location of the manifest or other definition files.
- ```schedule.interval```: Specifies how often to check for new versions.

Here's an example of a ```dependabot.yml``` file:

```yaml
# Basic dependabot.yml file with
# configuration for two package managers

version: 2
updates:
  # Enable version updates for npm
  - package-ecosystem: "npm"
    # Look for `package.json` and `lock` files in the `root` directory
    directory: "/"
    # Check the npm registry for updates every day (weekdays)
    schedule:
      interval: "daily"
    groups:
      production-dependencies:
        dependency-type: "production"
      development-dependencies:
        dependency-type: "development"

  # Enable version updates for Docker
  - package-ecosystem: "docker"
    # Look for a `Dockerfile` in the `root` directory
    directory: "/"
    # Check for updates once a week
    schedule:
      interval: "weekly"
    groups:
      production-dependencies:
        dependency-type: "production"
      development-dependencies:
        dependency-type: "development"
```
