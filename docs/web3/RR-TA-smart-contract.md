# Round Robin Task Allocation smart contract 

This smart contract implements the logic behind the Round Robin algorithm. In order to do that it uses the following set of types, variables, events, modifiers, methods and errors:

## Types

### Task

The struct task has the following fields:
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

- __allocationIndex__: needed to remove task when being reallocated.
- __endDate__: indicate when the task should be reasigned.
- __status__: the current status of the task.
- __rejecters__: list of users who rejected the task.
- __reallocationTime__: indicate how often, in seconds, the task will be reasigned.

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

- __benefits__: to be used in the future to award users for tasks completed
- __exists__: check if the user exists in the mapping
- __allocatedTasks__: list of tasks assigned to the user



## Variables


## Events

- Task created: 
    
    __TaskCreated(bytes32 indexed taskId)__

- Task deleted:
 
    __TaskDeleted(bytes32 indexed taskId)__

- Task accepted: 

    __TaskAccepted(bytes32 indexed userId, bytes32 indexed taskId)__

- Task rejected: 

    __TaskRejected(bytes32 indexed userId, bytes32 indexed taskId)__

- Task allocated:

    __TaskAllocated(bytes32 indexed userId, bytes32 indexed taskId, bytes32 previousUserId)__

- User registered: 

    __UserRegistered(bytes32 indexed userId)__

- User deleted: 
    
    __UserDeleted(bytes32 indexed userId)__

- Rejecter deleted:

    __RejecterDeleted(bytes32 indexed userId, bytes32 indexed taskId)__

## Modifiers

- userHasNoTask(bytes32 _userId): checks that the user doesn't hve a task assigned.
- userDontExist(bytes32 _userId): checks that the user doesn't exists.
- userExists(bytes32 _userId): checks that the user exists.
- taskDontExist(bytes32 _taskId): checks that the task doesn't exist.
- taskExists(bytes32 _taskId): checks that the task exists.
- taskAssigned(bytes32 _taskId, bytes32 _userId): checks that the task is been assigned
- tooManyTasks(bytes32 _userId): checks if the user exceeds the max number of assigned tasks.


## Methods

- __restart__() override external 
    
    Function used to clean up the contract. Removes tasks, task rejecters, resset task status, users and user index.

    
- __registerUser__(bytes32 _userId) external userDontExist(_userId)

    Registers an empty user given an ID.

- __createTask__(bytes32 _taskId, uint256 reallocationTime) external taskDontExist(_taskId)

    Creates an empty task given an ID.

- __allocateTask__(bytes32 _taskId, bytes32 _userId) external taskExists(_taskId) userExists(_userId)
        
    Calls the function that assigns a task to a user

- __acceptTask__(bytes32 _userId, bytes32 _taskId) external userExists(_userId) taskAssigned(_taskId, _userId) userHasNoTask(_userId)

    Function called when a user accepts a task

- __rejectTask__(bytes32 _userId, bytes32 _taskId) external userExists(_userId) taskAssigned(_taskId, _userId)
    
    Function used when a user rejects a task


- __reallocateTask__(bytes32 _taskId) public taskExists(_taskId)

    Fucntion that implements the round-robin algorithm

- __addUserAllocatedTask__(
    
    Function used to assign a task to a user

- __deleteUserAllocatedTask__(
- __getUser__(
- __getAllocatedTask__(
- __getTask(bytes32 _taskId)__
- __getRejecter__(bytes32 _taskId, bytes32 _userId)
- __getUserLength__()


## Errors

- TASK_ALREADY_ASSIGNED
- USER_HAS_TASK
- USER_ALREADY_EXISTS
- USER_DONT_EXIST
- TASK_EXISTS
- TASK_DONT_EXIST
- TASK_ALLOCATION_FAIL
- TASK_NOT_ASSIGNED_TO_USER
- USER_HAS_TOO_MANY_TASKS

!!! important "A feature that needs to be developed" 
    Cool and core feature.

!!! warning "A feature that would improve the prototype and doesn't require a great effort" 
    Cool and light feature.

!!! error "A feature that would improve the prototype but also requires a great effort" 
    Cool but heavy feature.

## Development scope
The Task Allocation Prototype (TAP) will simulate two scenarios:

- **First come first serve (FCFS)**: in this scenario the users have a feed of available tasks. The first user to successfully send a confirmation transaction will get the tasks assigned. Therefore there will be a lot of transactions that will resolve as error when a late request arrives. Once a tasks has been assigned to the user the feed is hidden and only the assigned task is shown.

- **Round robin