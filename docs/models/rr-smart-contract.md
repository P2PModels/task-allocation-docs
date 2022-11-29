# Round Robin Task Allocation smart contract

This smart contract implements the logic behind the Round Robin algorithm. In order to do that it uses the following set of types, variables, events, modifiers, methods and errors:

## Types

### Task

```
    struct Task {
        uint256 userIndex;
        uint256 allocationIndex;
        uint256 endDate;
        Status status;
        mapping(bytes32 => bool) rejecters;
        uint256 reallocationTime;
    }
```

- _allocationIndex_: needed to remove task when being reallocated.
- _endDate_: timestamp **in s** (when working with it in js remember to multiply by 1000!) of the task deadline.
- _status_: the current status of the task.
- _rejecters_: list of users who rejected the task.
- _reallocationTime_: the period of time **in s** in which the task has to be reallocated.

### User

```
struct User {
        uint256 index;
        uint256 benefits;
        bool available;
        bool exists;
        mapping(uint256 => bytes32) allocatedTasks;
        uint256 allocatedTasksLength;
    }
```

- _benefits_: in the future could taken into account by the algorithm, currently not used.
- _available_: whether the user is available (no task accepted) or bussy (task accepted).
- _exists_: check if the user exists in the mapping.
- _allocatedTasks_: list of tasks assigned to the user.
- _allocatedTasksLength_: length of the allocatedTask list.

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

### Task rejected

```
TaskRejected(bytes32 indexed userId, bytes32 indexed taskId)
```

### Task allocated

```
TaskAllocated(bytes32 indexed userId, bytes32 indexed taskId, bytes32 previousUserId)
```

### User registered

```
UserRegistered(bytes32 indexed userId)
```

### User deleted

```
UserDeleted(bytes32 indexed userId)
```

### Rejecter deleted

```
RejecterDeleted(bytes32 indexed userId, bytes32 indexed taskId)
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

### taskAssigned

```
 taskAssigned(bytes32 _taskId, bytes32 _userId)
```

Checks that the task is been assigned.

### tooManyTasks

```
 tooManyTasks(bytes32 _userId)
```

Checks if the user exceeds the max number of assigned tasks.

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

### Allocate task

allocateTask(bytes32 \_taskId, bytes32 \_userId) &rarr; _void_

<div class="badge-container">
    <div class="badge badge-external">external</div>
</div>

Calls the function that assigns a task to a user

Modifiers:

- taskExists(\_taskId)
- userExists(\_userId)

Events:

- TaskAllocated(\_userId, \_taskId, oldUserId)


### Reallocate task

reallocateTask(bytes32 \_taskId) &rarr; _void_

<div class="badge-container">
    <div class="badge badge-public">public</div>
</div>

Fucntion that implements the round-robin algorithm:

      - Delete task from the previous "owner"
      - Iterate until find a user to whom assign the task or the array of users was totally traversed
          - Check if index arrives to the end of the round then it should start over
          - Try to assigned that task to user (currUserId)
          - If assignation was successful emit event TaskAllocated
          - If assignation did not work, increase counters to continue with the round robin
      - Assign rejected status to the task if it couldn't be assigned to a user

Fisrt the algorithm loads the current task, which contains the previously assigned user (by index).
Then loads the old user ID, generates de new user index (adding one to the old one), sets a flag for founded asignee and sets a counter to 0.

Then the algorithm starts a while loop to traverse all the users while no asignee is founded.
Inside the loop it first checks that the index it's within range, if greater is restarted.
Then it gets the user ID by index.
Trys to assign the task to the user. (The task is assigned if the user is available, she doesn't have the task already, doesn't have max number of tasks and she hasn't rejected it)
Checks if it worked, if not the user counter adds one aswell as the new user index.

If the loop fails to find an asignee, the task status is set to rejected.

Modifiers:

- taskExists(\_taskId)

Events: 

- TaskAllocated(\_userId, \_taskId, oldUserId)

### Reject task

rejectTask(bytes32 \_userId, bytes32 \_taskId) &rarr; _void_

<div class="badge-container">
    <div class="badge badge-external">external</div>
</div>

Function used when a user rejects a task

Modifiers:

- userExists(\_userId)
- taskAssigned(\_taskId, \_userId)

Events: 

- TaskRejected(\_userId, \_taskId)

### Add user allocated task

addUserAllocatedTask(bytes32 _userId, bytes32 _taskId)  &rarr; _bool_

<div class="badge-container">
    <div class="badge badge-private">private</div>
</div>        

  Function used to assign a task to a user

- **deleteUserAllocatedTask**(
- **getUser**(
- **getAllocatedTask**(
- **getTask(bytes32 \_taskId)**
- **getRejecter**(bytes32 \_taskId, bytes32 \_userId)
- **getUserLength**()

## Errors

#### USER_HAS_TASK

#### USER_ALREADY_EXISTS

#### USER_DONT_EXIST

#### USER_HAS_TOO_MANY_TASKS

#### TASK_EXISTS

#### TASK_DONT_EXIST

#### TASK_ALLOCATION_FAIL

#### TASK_NOT_AVAILABLE

#### TASK_NOT_ASSIGNED_TO_USER
