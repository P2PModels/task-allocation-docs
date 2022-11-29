# Subgraph

A subgraph for the The Graph protocol has been developed. Therefore a Graphql endpoint is exposed to be queried by the client app.

## Entities

### Task

```graphql
type Task @entity {
  id: ID!
  userId: String!
  status: TaskStatus!
}
```

Main entity, tracks the current status of the task and the user that has accepted it.

### User

```graphql
type User @entity {
  id: ID!
  hasTask: Boolean!
}
```

Generic user entity, also contains a flag to track whether the user is available (no task accepted) or bussy (task accepted).

## Enums

```graphql
enum TaskStatus {
  NonExistent
  Available
  Accepted
  Completed
}
```
