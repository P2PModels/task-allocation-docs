# Subgraph

A subgraph for the The Graph protocol has been developed. Therefore a Graphql endpoint is exposed to be queried by the client app.

## Entities

### Task

```graphql
type Task @entity {
  id: ID!
  endDate: BigInt!
  status: TaskStatus!
  reallocationTime: BigInt!
  assignee: User
  rejecterUsers: [User]! @derivedFrom(field: "rejectedTasks")
}
```

- _endDate_: timestamp **in s** (when working with it in js remember to multiply by 1000!) of the task deadline.
- _status_: current status of the task.
- _reallocationTime_: the period of time **in s** in which the task has to be reallocated. It changes with task priority. In the current version the user is not aware of this feature.
- _assignee_: user to whom the task has been assaigned or that has accepted it.
- _rejecterUsers_: list of users that have rejected the task so it isn't assigned to them again.

### User

```graphql
type User @entity {
  id: ID!
  benefits: BigInt!
  available: Boolean!
  rejectedTasks: [Task]!
}
```

- _benefits_: in the future could taken into account by the algorithm, currently not used.
- _available_: whether the user is available (no task accepted) or bussy (task accepted).
- _rejectedTasks_: list of tasks that the user has rejected.

## Enums

```graphql
enum TaskStatus {
  NonExistent
  Available
  Assigned
  Accepted
  Rejected
  Completed
}
```
