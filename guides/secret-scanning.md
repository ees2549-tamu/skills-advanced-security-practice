# Secret Scanning

Secret scanning is a GitHub Advanced Security feature that scans repositories for known types of secrets. 
It prevents the fraudulent use of secrets that were committed accidentally.

## How does secret scanning work?

Secret scanning automatically scans your entire Git history on all branches present in your GitHub repository for any secrets. 
Additionally, secret scanning scans:
- Descriptions and comments in issues.
- Titles, descriptions, and comments, in open and closed historical issues.
- Titles, descriptions, and comments in pull requests.
- Titles, descriptions, and comments in GitHub Discussions.

When a secret with a known pattern is committed into a private or public repository in your project, secret scanning sends a notification to all repository administrators about the commit that contains the secret. 
Repository administrators can then view the list of all detected secrets in the repository's Security tab.

<img width="1145" height="551" alt="image" src="https://github.com/user-attachments/assets/4d9f2e9f-022b-4aa1-9f6d-9df24ad97b69" />

## Push Protection

Push protection prevents secret leaks by scanning for highly identifiable secrets before they're pushed. 
When a secret is detected in code, contributors are prompted directly in their IDE or command-line interface with remediation guidance to ensure that the secret isn't inadvertently exposed. 
To proceed, contributors must either remove the secret(s) from the push or, if needed, bypass the protection.

Push protection for users is on by default for public projects, and automatically protects you from accidentally committing secrets to public repositories across GitHub.

## Validity Checks

Validity checks determine whether a token is still active and, when possible, whether it was ever active. 
This is useful when you're deciding how to remediate an exposure. 
For example, you might prioritize remediating active secrets before checking your security logs for unauthorized access via API keys that have already been revoked.

## Quick Facts

- Secret scanning alerts for users are available for free on all public repositories.
- Organizations with a license for GitHub Advanced Security can also enable secret scanning on their private and internal repositories.
- Secret scanning is enabled by default on public repositories and can't be configured or turned off. If you want to configure or disable secret scanning on a public repository, you must switch the repository to a private one with GitHub Advanced Security.
- Secret scanning must be enabled manually on private repositories. This module's Configure secret scanning unit covers how to do this.
- Secret scanning is not available on private repositories without GitHub Advanced Security.
- Alerts from secret scanning can be enabled or disabled where available.

## How do I enable secret scanning for a repository?

Follow these steps to enable _secret scanning_ and _push protection_ on a private repository:

1. In your repository, navigate to **Settings**.
2. In the **Security** section, select **Advanced Security**.
3. Select the **Enable** button next to **Secret Protection**.
4. Review the impact of enabling and select **Enable Secret Protection**.
    - If you see a **Disable** button, it means that secret scanning was already enabled at organization level.
5. Select the **Enable** button next to **Push protection**.

## How do I exclude files from being scanned?

You can create a `.github/secret_scanning.yml` file in your repository that excludes some directories from being scanned.
In the file, use `paths-ignore` followed by the paths you want to exclude from secret scanning. An example:

```yaml
paths-ignore:
  - "foo/bar/*.js"
```

**NOTE**: Only the first 1,000 entries in `paths-ignore` will be excluded from scans. 
Additionally, if the `secret_scanning.yml` file is larger than 1 MB, secret scanning will ignore the entire file.

## How do I configure the recipients of secret scanning alerts?

Repository and organization administrators can give view access to security alerts to people or teams who have write access to the repository under **Settings** > **Security** > **Advanced Security** > **Access to Alerts**.
If you want to give view access to security alerts to additional people in your team, type their name in the **Search for people of teams** field, select their name in the list of matches that appear, and select **Save changes**.

## Secret protection settings

- **Validity checks** – Verifies whether exposed secrets are still active by querying the relevant provider.
- **Non-provider patterns** – Scans for custom or non-partnered secret formats beyond the standard provider patterns.
- **Scan for generic passwords** – Uses AI to detect weak or generic passwords in your code.
- **Push protection** – Blocks commits containing supported secret types and prevents them from being pushed.
- **Bypass rules** – Let specific roles or teams bypass push protection and review bypass requests.
- **Alert dismissal rules** – Require justification before users can dismiss alerts (if enabled).
- **Custom patterns** – Define up to 100 custom patterns to detect internal secrets.

To access these options, go to **Settings** > **Code security and analysis** > **Secret Protection** on your repository or organization.
