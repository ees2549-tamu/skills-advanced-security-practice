# GitHub Advanced Security (GHAS)

The following information covers commonly asked questions and guidance on how to setup GitHub Advance Security (GHAS) features for a GitHub repository (referenced from Microsoft Learn's [_Introduction to GitHub Advanced Security_](https://learn.microsoft.com/en-us/training/modules/introduction-github-advanced-security/) course)

## What is GitHub Advanced Security?

**GitHub Advanced Security** (or **GHAS**) is an application security solution that helps developers secure their code and manage risks without disrupting their workflow.
3 key features of GHAS that assist teams stay on top of the latest security threats are Secret scanning, Code scanning, and Dependabot.

## What is Secret scanning?

**Secret scanning** is a critical GitHub security feature that identifies and helps prevent the accidental exposure of sensitive information, such as API keys and tokens, within your source code.
Secret scanning is available for all public repositories for free, and can also be enabled for private repositories with a GitHub Advanced Security (GHAS) license.

### What secret scanning does:
- Helps prevent unauthorized access and protects confidential data. 
- Operates by searching for predefined patterns and signatures indicative of sensitive information, ensuring that potential security risks are promptly addressed. By default, secret scanning looks for highly accurate patterns that have been provided by a GitHub Partner (custom patterns can be created for other use cases).
- Detects exposed secrets, allowing teams to revoke or rotate them as early as possible—often before they can be used for malicious purposes, reducing the risk of data breaches and preserving confidentiality throughout development. This is crucial for the secure software development life cycle.

### Secret scanning as a feature includes:
- Push protection proactively prevents secret leaks by scanning code on commit and blocking a push if a secret is present.
- The ability to easily view alerts and remediate them without ever having to leave GitHub.

## What is Code scanning?

Code scanning is an integral feature of GHAS that analyzes source code for security vulnerabilities and coding errors.

### What code scanning does:

- Code scanning employs static analysis techniques to identify potential threats such as:
  - SQL injection
  - Cross-site scripting (XSS)
  - Buffer overflows
- Provides automated feedback directly within the pull request workflow to enable developers to address vulnerabilites early in the development process.
- Detects vulnerabilities that may already exist in a production environment

## What is Dependabot?

Dependabot is an automated dependency management tool, responsible for keeping project dependencies up-to-date.

### Dependabot can:
- Regularly check for updates to libraries and frameworks used in a project
- Automatically opens pull requests to update dependecies to their latest, secure version
- Work closely with the Dependency Graph to determine which dependencies are in use and cross-reference them against the GitHub Advisory Database to detect vulnerabilities.

### Dependabot includes:
- Alerts for known vulnerabilities
- Security updates for vulnerable packages
- Version updates to keep dependencies current
- Dependency Review, enabling users to preview any vulnerable packages introduced in a PR and prevent their addition before merging

## Where do you enable Secret scanning, Code scanning, and Dependabot alerts?

To enable any of the alerts from a repository level first navigate to your repository’s security tab.

<img width="1158" height="61" alt="image" src="https://github.com/user-attachments/assets/e8b6bec9-78d6-4ee7-9eb0-0e8aa107cd63" />

Next, enable your alerts in the Security overview.

<img width="1333" height="505" alt="image" src="https://github.com/user-attachments/assets/f8f54175-463b-4c80-b821-7fcd284e7823" />

