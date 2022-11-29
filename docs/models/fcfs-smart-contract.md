# Smart contract

This smart contract implements the logic behind the First Comes First Serve algorithm. In order to do that it uses the following set of types, events, modifiers, methods and errors:

## Types

### Task statuses

```
    enum Status {
        NonExistent,
        Available,
        Accepted,
        Completed
    }
```

### Task

```
    struct Task {
        uint256 userIndex;
        uint256 endDate;
        Status status;
    }
```

- _endDate_: indicate when the task should be reasigned.
- _status_: the current status of the task.reasigned.

### User

```
struct User {
        uint256 index;
        bool exists;
    }
```

- _exists_: check if the user exists in the mapping

## Events

### Task created

```
TaskCreated(bytes32 indexed taskId)
```

### Task deleted

```
TaskDeleted(bytes32 indexed taskId)
```

### Task accepted

```
TaskAccepted(bytes32 indexed userId, bytes32 indexed taskId)
```

### User registered

```
UserRegistered(bytes32 indexed userId)
```

### User deleted

```
UserDeleted(bytes32 indexed userId)
```

## Modifiers

### userHasNoTask

```
 userHasNoTask(bytes32 _userId)
```

Checks that the user doesn't have a task assigned.

### userDontExist

```
 userDontExist(bytes32 _userId)
```

Checks that the user doesn't exists.

### userExists

```
 userExists(bytes32 _userId)
```

Checks that the user exists.

### taskDontExist

```
 taskDontExist(bytes32 _taskId)
```

Checks that the task doesn't exist.

### taskExists

```
 taskExists(bytes32 _taskId)
```

Checks that the task exists.

### taskAvailable

```
 taskAvailable(bytes32 _taskId)
```

Checks that the task status is available.

## Methods

### Restart

restart() &rarr; _void_

<div class="badge-container">
    <div class="badge badge-override">override</div>
    <div class="badge badge-external">external</div>
</div>

Function used to clean up the contract. Removes tasks, resets task status, removes users and user index.

Events:

- TaskDeleted(\_taskId)
- UserDeleted(\_userId)
- TasksRestart(msg.sender)

### Register user

registerUser(bytes32 \_userId) &rarr; _void_

<div class="badge-container">
    <div class="badge badge-external">external</div>
</div>

Registers an empty user given an ID.

Modifiers:

- userDontExist(\_userId)

Events:

- UserRegistered(\_userId)

### Create task

createTask(bytes32 \_taskId, uint256 reallocationTime) &rarr; _void_

<div class="badge-container">
    <div class="badge badge-external">external</div>
</div>

Creates an empty task given an ID.

Modifiers:

- taskDontExist(\_taskId)

Events:

- TaskCreated(\_taskId)

### Accept task

acceptTask(bytes32 \_userId, bytes32 \_taskId) &rarr; _void_

<div class="badge-container">
    <div class="badge badge-external">external</div>
</div>

Function called when a user accepts a task

Modifiers:

- userExists(\_userId)
- taskAssigned(\_taskId, \_userId)
- userHasNoTask(\_userId)

Events:

- TaskAccepted(\_taskId)

## Errors

#### USER_HAS_TASK

#### USER_ALREADY_EXISTS

#### USER_DONT_EXIST

#### TASK_EXISTS

#### TASK_DONT_EXIST

#### TASK_ALLOCATION_FAIL

#### TASK_NOT_AVAILABLE
