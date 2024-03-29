# Roadmap

In this document we want to write down the features we are considering for development. We use the INVEST principles for that, based in "How to write user stories" by Stormotion
Note: we should define which features we need to develope to test our idea and whitch features we could simulate. As an example we could simulate the register page and provide previously created users to testers. We will rank features by importance like this:

!!! important "A feature that needs to be developed"
Cool and core feature.

!!! warning "A feature that would improve the prototype and doesn't require a great effort"
Cool and light feature.

!!! error "A feature that would improve the prototype but also requires a great effort"
Cool but heavy feature.

## Development scope

The Task Allocation Prototype (TAP) will simulate two scenarios:


    - **First come first serve (FCFS)**: in this scenario the users have a feed of available tasks. The first user to successfully send a confirmation transaction will get the tasks assigned. Therefore there will be a lot of transactions that will resolve as error when a late request arrives. Once a tasks has been assigned to the user the feed is hidden and only the assigned task is shown.


    - **Round robin + availability calendar (RR+cal)**: this prototype implements a task assignment method based on the Round Robin algorithm: Each new available translation task is automatically assigned to a linguist for a period of time during which it can be accepted or rejected. If the task is rejected or if time runs out, the task is then passed on to another linguist. The algorithm continues to iterate back and forth over each linguist until the task is accepted by one or rejected by all. Also, in this scenario the user has aaccess to a calenar to select her working hours in the week. Taking this into account, the smart contract will assign tasks to users based in the round robin algorithm and working hours.

---

## Milestone | **TAP** - v2.0 &check;

### Epic: **Refactoring: removing Aragon dependencies** &check;

!!! important "As a developer I want to have a simpler smart contract (dependencies wise) so I can develope faster and mantain less." 
    - The smart contract doesn't use Aragon stack. 
    - The smart contract uses SafeMath from Zeplin. 
    - The smart contract has al the functionalities needed for the round robin algorithm. 
    - There a is a test suit for the new smart contract.

!!! important "As a developer I want to connect the webapp directly to The Graph so I can develope faster and mantain less." 
    - The suubgraph doesn't use Aragon connector. 
    - The webapp hooks implement the logic necessary to directly connect to The Graph. Fake subscriptions implemented by Aragon connector are changed by query pooling.

#### Epic: User landing page update &check;

!!! important "As a user I want to see an updated design so that I can have a better user experience" 
    - The header of the site is containerized. 
    - A footer is added to the page.

!!! important "As a user I want to have an onboarding process so that I can get informed of the features of the prototype" 
    - An onboarding process is started the first time the users access the website.

---

## Milestone | **TAP First Come First Serve** - v2.0 &check;

#### Epic: Web3 implementation of the model &check;

!!! important "As a user I want to be able to access the FCFS model deployed on the blockchain so I can audit the algorithm." 
    - There is a smart contract that implements the FCFS model 
    - There is a test suit for the smart contract that verifies that the implementation is correct.

!!! important "As a user I want to be able to access refined data from the FCFS smart contract deployed on the blockchain so I can have a better user experience." 
    - There is a subgraph that process the FCFS smart contract events.

#### Epic: Admin page for FCFS model &check;

!!! important "As an administrator I want to be able to restart the prototype so I can prepare the prototype for user testing with a few clicks and no previous knowledge." 
    - There is an admin page with a restart prototype button that automatically restores the initial state of the mock data in the smart contract.

!!! important "As an administrator I want to be able to see how many users exist, their id and if they already have a task assigned so I can monitor the current users while the user test is running." 
    - There is a table with the current users, their id and availability.

!!! important "As an administrator I want to be able to see how many tasks exist, their id, status and to whom are assigned so I can monitor the tasks while the user test is running." 
    - There is a table with the current tasks, their id, status and the user id of the assigned user.

!!! important "As an administrator I want to be able to see the procesed transactions while restarting the prototype so I can have feedback for its progress." 
    - There is a table with the current transactions, their hash, from account address and to account address.

#### Epic: User landing page for FCFS model &check;

!!! important "As a user I want to be able to see a short description of the current distribution model so I can be informed." 
    - A banner with a description of the current model its shown in the user landing page.

!!! important "As a user I want to be able to see only the tasks available so I can focus on choosing the following task" 
    - All the available tasks are shown to the user.

#### Epic: Select current model &check;

!!! important "As a user I want a config page where I can set the model and the user id so I can test the different models." 
    - There is a config page available under /config. 
    - The webapp redirects to the config page if / is visited. 
    - The user can set the model and user id from a select input field.

!!! important "As a user I want to be able to test the different models from the home page given the proper configuration so I can have a better experience." 
    - The home page consumes the config params from the url and then chnges the ui based on it.

!!! important "As an admin I want to be able to share a link with the user and model configured so I can ease the users experience." 
    - There is a share link button 
    - There is a link that navigates to the home page with url params to set user and model

!!! warning "As an administrator I want to be able to select the current model so I can set the proper conditions for experiments" 
    - The algorithm used (smart contract) is selected from the admin page. 
    - The interface of the webapp changes taking the algorithm used into account.

---

## Milestone | **TAP Round Robin** - v2.0 &check;

### Epic: Web3 implementation of the model &check;

!!! important "As a user I want to be able to access the RR model deployed on the blockchain so I can audit the algorithm." 
    - There is a smart contract that implements the RR model 
    - There is a test suit for the smart contract that verifies that the implementation is correct.

!!! important "As a user I want to be able to access refined data from the RR smart contract deployed on the blockchain so I can have a better user experience." 
    - There is a subgraph that process the RR smart contract events.

### Epic: User landing page &check;

!!! important "As a user I want to be able to see a short description of the current distribution model so I can be informed." 
    - A banner with a description of the current model its shown in the user landing page.

!!! important "As a user I want to be able to see only the tasks assigned to me so I can focus on choosing the following task" 
    - If no tasks has been accepted by the user yet, only the available tasks will be shown.

!!! important "As a user I want to be able to see only the task accepted so I can focus on my current job" 
    - If a task has been accepted by the user, only the card of the accepted task will be shown.

### Epic: Admin page for RR model &check;

!!! important "As an administrator I want to be able to restart the prototype so I can prepare the prototype for user testing with a few clicks and no previous knowledge." 
    - There is an admin page with a restart prototype button that automatically restores the initial state of the mock data in the smart contract.

!!! important "As an administrator I want to be able to see how many users exist, their id and if they already have a task assigned so I can monitor the current users while the user test is running." 
    - There is a table with the current users, their id and availability.

!!! important "As an administrator I want to be able to see how many tasks exist, their id, status, timer and to whom are assigned so I can monitor the tasks while the user test is running." 
    - There is a table with the current tasks, their id, status and the user id of the assigned user.

!!! important "As an administrator I want to be able to see the processed transactions while restarting the prototype so I can have feedback for its progress." 
    - There is a table with the current transactions, their hash, from account address and to account address.

---

## Milestone | **TAP Round Robin + calendar ** - v2.0 &check;

### Epic: **Calendar** &check;

!!! important "As a user I want to be able to select my working hours so I can get available tasks while I'm working"
    - The algorithm takes into account if the user is working.
    - The webapp has a calendar in which the user can select her working hours.

!!! important "As a user I want to be able to set my availability and store it in the smart contract so that the algorithm automatically takes that into account" 
    - The smart contract implements a data structure to take availability of users into account. 
    - A test suit is available for the new version of the smart contract.

!!! important "As a user I want to be able to configure my working hours through the webapp so that I don't need technical knowledge about the blockchain."
    - The subgraph entities are updated with new fields 
    - The subgraph listens to new events

!!! important "As a user I want to be able see a calendar with week days and hours slots so I can plan working hours." 
    - There is a button in the user landing page that opens a calendar popup. 
    - There is a calendar with week days and hours slots.

!!! important "As a user I want to be able select hours slots so I can save my working hours." 
    - The user can click and drag in hours slots to select working hours of the week. 
    - There is a button to save the working hours.

!!! important "As a user I want to be notified that the selected hours have been stored so I can be informed." 
    - A notifications pops up once the schedule has been stored.

!!! important "As a user I want to be notified if the storage of my schedule fails so I can take action." 
    - A notifications pops up once the storage action has failed.

---

## Milestone | **Agents**

### Epic: Simple e2e testing to simulate real agent 

!!! important "As an administrator I want to be able to launch a suit of e2e test so that I can verify that the prototype is working correctly" 
    - There is an end-to-end test suit covering all the actions the users can do

### Epic: Multiple agents

!!! warning "TODO" 
    - TODO
