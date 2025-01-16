The platform makes heavy use of the [graphql-ruby](https://graphql-ruby.org/) gem to define, implement, and execute GraphQL queries and mutations.

- Types are defined in [app/graphql/types](https://github.com/eLearning-Plus/MemberHub/tree/main/app/graphql/types)
- Query resolvers are defined in [app/graphql/queries](https://github.com/eLearning-Plus/MemberHub/tree/main/app/graphql/queries)
- Mutations are defined in [app/graphql/mutations](https://github.com/eLearning-Plus/MemberHub/tree/main/app/graphql/mutations)

The root query type can be found at [app/graphql/types/query_type.rb](https://github.com/eLearning-Plus/MemberHub/tree/main/app/graphql/types/query_type.rb)

The GraphQL schema can be explored with the GraphQL explorer, which is made available in the rails container and is accessible at the following url after performing `docker-compose up` in the API repository root directory:

`http://127.0.0.1/graphiql`

Where possible, we attempt to follow the [Relay connections specification](https://relay.dev/graphql/connections.htm), allowing for curor-based pagination, and in some cases, adding extra data to the edges between two types (e.g. `UserContentEdgeType` defines the data available on the 'edge' between `User`s and `ContentItem`s).