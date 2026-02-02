# GraphQL API

The GraphQL API allows you to export a list of your dependencies that you can save as a CSV and then import into a Business Intelligence tool for analysis. 
You can use the API to quickly audit the known vulnerabilities of dependencies across your organizations.

You'll need to create an OAuth token with the following scopes to communicate with the GraphQL server:
- `user`
- `public_repo`
- `repo`
- `repo_deployment`
- `repo:status`
- `read:repo_hook`
- `read:org`
- `read:public_key`
- `read:gpg_key`

The GraphQL API has a single endpoint that doesn't change:

`https://api.github.com/graphql`

## GraphQL Explorer

The GraphQL Explorer is the recommended tool for communicating with the GraphQL API. 
The GraphQL Explorer is a "graphical interactive in-browser GraphQL IDE". 
The Explorer is an instance of [GraphiQL App](https://github.com/skevy/graphiql-app).

After downloading the GraphiQL app, follow these instructions to configure it:

1. Get a properly configured OAuth token.
2. Open GraphiQL.
3. In the upper-right corner of GraphiQL, select **Edit HTTP Headers**.
4. In the **Key** field, enter 'Authorization'. In the Edit HTTP Headers field, enter `Bearer <token>`, where `<token>` is your generated OAuth token.
5. Select the checkmark to the right of the token to save it.
6. To return to the editor, select outside of the **Edit HTTP Headers** modal.
7. In the **GraphQL Endpoint** field, enter `https://api.github.com/graphql`.
8. In the **Method** drop-down, select Post.

## GraphQL Queries

GraphQL queries return only the data you specify. 
When you're forming a query, you must specify fields within fields (also known as nested subfields) until you return only scalars (primitive values like integers, float, string, boolean, or GitHub object IDs).

Queries are structured like this:

```graphql
query {
  JSON objects to return
}
```

### Example API query

The following code block is an example of a complex API query that fetches the vulnerable dependency for a repository.

```graphql
query {
  repository(name: "${repo}", owner: "${org}") { 
    vulnerabilityAlerts(first: 100) {
      nodes { 
        createdAt 
        dismissedAt 
        securityVulnerability { 
          package { 
            name 
          } 
          severity 
          vulnerableVersionRange 
          advisory { 
            ghsaId 
            publishedAt 
            identifiers { 
              type 
              value 
            } 
          } 
        } 
      } 
    } 
  }
}
```

And here is what each of these components of the query are and do:

```graphql
query
```

Your goal is to read data from the server, not to modify it, query is the root operation. 
(If you don't specify an operation, query is also the default.)

```graphql
repository (name: "${repo}", owner: "${org}") {
```

Begin the query by finding a repository object. 
The schema validation indicates this object requires an owner and a name argument.

```graphql
vulnerabilityAlerts(first: 100) {
```

The vulnerabilityAlerts object accounts for all Dependabot alerts in the repository. 
Schema validation indicates this object requires a last or first number of results as an argument, this example uses 100.

```graphql
nodes {
```

Retrieve the nodes at the end of the edge.

```graphql
createdAt 
dismissedAt 
securityVulnerability { 
  package { 
    name 
  } 
  severity 
  vulnerableVersionRange 
  advisory {
```

For the nodes, specify the objects to return, in this case `createdAt`, `dismissedAt` and `securityVulnerability`.

```graphql
ghsaId 
        publishedAt 
        identifiers { 
          type 
          value 
        } 
      } 
    } 
  } 
}
```

Specify the `ghsaId`, `publishedAt`, and `identifiers` fields of the advisory object. 
The `identifiers` field has the type `type` and `value`.

Information about resolved alerts isn't stored in the API and can't be retrieved.
