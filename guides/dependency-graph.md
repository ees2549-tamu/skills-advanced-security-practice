# Dependency Graph

<img width="1807" height="914" alt="image" src="https://github.com/user-attachments/assets/8eb8211c-c5d5-4c93-85fa-4c4004f1c7fc" />

The dependency graph is a summary of the manifest and lock files stored in a repository and any dependencies that are submitted for the repository using the Dependency submission API. 
These files contain metadata about your project. 

The dependency graph is automatically generated for public repositories and includes the following information:
- Dependencies, which are the ecosystem and packages on which the repository depends.
- Dependents, which are the repositories and packages that depend on the repository.

The dependency graph uses the information from your lock and manifest files to provide a list of two kinds of dependencies:
- The direct dependencies explicitly defined in a manifest or lock file or submitted with the Dependency submission API.
- The indirect dependencies, also known as transitive dependencies or subdependencies, which are dependencies used by packages that are dependencies of your project.

## What are lock files?

**Lock files** (or their equivalent) generate the most reliable dependency graph, because they define exactly which versions of the direct and indirect dependencies you currently use. 
By using lock files, you ensure that all contributors to the repository are using the same versions, making it easier for you to test and debug code. 
If your ecosystem doesn't have lock files, you can use premade actions that resolve transitive dependencies for many ecosystems.

## Enable the dependency graph for private repositories

As a repository administrator, you can also choose to enable the dependency graph for private repositories by completing these steps:

1. Go to your GitHub repository.
2. Select your repository Settings.
3. On the left-hand menu under Security, select Advanced Security.
4. In the Dependency graph section, select Enable.

## How do I view the dependency graph?

You can view the dependency graph for your repository by following these steps:

1. Go to your GitHub repository.
2. Select your repository Insights.
3. Select Dependency graph.
4. You can select the Dependencies or Dependents tab from the Dependency graph view.

<img width="1807" height="865" alt="image" src="https://github.com/user-attachments/assets/4b5279f9-b893-4ed7-91ed-a9895b468e31" />
