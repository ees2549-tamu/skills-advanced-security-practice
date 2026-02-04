# Code Scanning

Code scanning uses CodeQL to analyze the code in a GitHub repository to find security vulnerabilities and coding errors. 
Code scanning is available for all public repositories, and for private repositories owned by organizations where GitHub Advanced Security is enabled. 
If code scanning finds a potential vulnerability or error in your code, GitHub displays an alert in the repository's Security tab. 
After you fix the code that triggered the alert, GitHub closes the alert.

## What is CodeQL?

CodeQL is the code analysis engine GitHub developed to automate security checks. 
You can analyze your code using CodeQL and display the results as code scanning alerts. 

There are three main ways to set up CodeQL analysis for code scanning:
- Use default setup to quickly configure CodeQL analysis for code scanning on your repository. The default setup handles choosing the languages to analyze, query suite to run, and events that trigger scans with the option to manually configure the languages and query suites. This setup option runs code scanning as a GitHub Action.
- Use advanced setup to add the CodeQL workflow directly to your repository. Adding the CodeQL workflow directly into your repository generates a customizable workflow file, which uses the [github/codeql-action](https://github.com/github/codeql-action/) to run the CodeQL CLI as a GitHub Action.
- Run the CodeQL CLI directly in an external CI system and upload the results to GitHub.

CodeQL supports both compiled and interpreted languages, and it can find vulnerabilities and errors in code written in the following supported languages:

- C or C++
- C#
- Go
- Java/Kotlin
- JavaScript/TypeScript
- Python
- Ruby
- Swift

## How do I enable CodeQL?

If you have write permissions to a repository, you can set up or configure code scanning for that repository.

### Using the default setup

Follow these steps to set up code scanning using the CodeQL GitHub Actions workflow:

1. Navigate to your repository's main page.
2. Under your repository name, select the **Security** tab.

<img width="999" height="79" alt="image" src="https://github.com/user-attachments/assets/2d816054-24a4-4843-b5e2-078f56961b10" />

3. Select **Set up code scanning**. 
    - If this option isn't available, ask an organization owner or repository administrator to enable GitHub Advanced Security.

<img width="840" height="135" alt="image" src="https://github.com/user-attachments/assets/7e91e24b-f0ef-4280-8783-3a4ec8350673" />

4. In the **Set up** drop-down, select **Default**.
5. Review the default options. If needed, select the **Edit** button in the bottom left corner of the new window to customize how CodeQL runs.
    - The on:pull_request and on:push triggers are the default for code scanning are each useful for different purposes. You'll learn more about these triggers in the Configure Code Scanning unit.
6. Select Enable CodeQL once you're ready to turn on code scanning.
    - In the default CodeQL analysis workflow, code scanning is configured to analyze your code each time you either push a change to any protected branches or raise a pull request against the default branch. Once the push is made, code scanning runs automatically.

### Using the Advanced setup

If you already have a repository set up to use code scanning using the default setup method, you can switch to using the Advanced setup in the settings. 
Navigate to the Code scanning section under **Settings** > **Code security and analysis**, and then select the three dots overflow icon (...). In the drop-down, select **Switch to advanced**. 
Then, follow the prompts to disable CodeQL, and re-enable it with the advanced setup's generated workflow file.

## How can I modify the code-scanning workflow?

GitHub saves workflow files in the `.github/workflows` directory of your repository. 
You can find a workflow you have added by searching for its file name. 
For example, by default, the workflow file for CodeQL code scanning is called `codeql-analysis.yml`.

Follow these steps to edit a workflow file:

1. To open the workflow editor, select the **Edit** icon in the upper-right corner of the file view.

<img width="1884" height="524" alt="image" src="https://github.com/user-attachments/assets/1e87d227-e14b-4f72-9e97-e066c9ad8b0f" />

2. Make your edits.

3. After you have edited the file, select **Commit changes** and complete the Commit changes form. You can choose to commit directly to the current branch, or create a new branch and start a pull request.

<img width="475" height="490" alt="image" src="https://github.com/user-attachments/assets/d190b8b7-c034-435e-90ef-c6fd32d35cd9" />

## How can I avoid unnecessary scans of pull requests?

You might want to avoid a code scan being triggered on specific pull requests targeted against the default branch, irrespective of which files have been changed. 
You can configure this setting by specifying `on:pull_request:paths-ignore` or `on:pull_request:paths` in the code-scanning workflow. 

For example, if the only changes in a pull request are to files with the file extensions `.md` or `.txt` you can use the following `paths-ignore` array:

```yaml
on:
   push:
      branches: [main, protected]
   pull_request:
      branches: [main]
      paths-ignore:
         - '**/*.md'
         - '**/*.txt'
```

## How do I adjust a scanning schedule?

If you use the default CodeQL analysis workflow, the workflow scans the code in your repository once a week at a randomly generated day and time, in addition to the scans triggered by events. 
To adjust this schedule, edit the `cron` value in the workflow.

The following example shows a CodeQL analysis workflow for a repository with a default branch called `main` and one protected branch called `protected`:

```yaml
on:
   push:
      branches: [main, protected]
   pull_request:
      branches: [main]
   schedule:
      - cron: '20 14 * * 1'
```

This workflow scans:
- Every push to the default branch and the protected branch
- Every pull request to the default branch
- The default branch every Monday at 14:20 UTC
