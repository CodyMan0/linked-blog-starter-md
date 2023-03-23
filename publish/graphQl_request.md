#### Why do I have to install `graphql`?

`graphql-request` uses methods exposed by the `graphql` package to handle some internal logic. On top of that, for TypeScript users, 


What's the difference between `graphql-request`, Apollo and Relay?

`graphql-request` is the most **minimal and simplest** to use [[graphQL_client]]. It's perfect for small scripts or simple apps.

Compared to GraphQL clients like Apollo or Relay, `graphql-request` **doesn't have a built-in cache** and has no integrations for frontend frameworks. The goal is to keep the package and API as minimal as possible.