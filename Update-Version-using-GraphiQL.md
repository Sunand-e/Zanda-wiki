To update the current version and force the frontend to load the latest version, follow these steps:

## Step 1: Log in as Super Admin

## Step 2: Access GraphiQL
- Open your browser and go to.
   - [`staging`](https://staging.zanda360.com/graphiql)
   - [`production`](https://app.zanda360.com/graphiql)

## Step 3: Run Mutation
- In the GraphiQL editor, search for the mutation `updateCurrentVersion`.
- Use the following mutation to update the version automatically with the current timestamp:

```graphql
mutation MyMutation {
  __typename
  updateCurrentVersion {
    message
    currentVersion {
      createdAt
      id
      updatedAt
      versionTimestamp
    }
  }
}
```
