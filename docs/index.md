# **Task Allocation prototype**

## Introduction

At P2PModels we are implementing a new version of the Task Allocation prototype with the following objectives:

- Remove Aragon from the stack.
- Implement a new feature for the Round Robin model (add calendar availavility).
- Improve admin experience by implementing a complete web interface to manage the prototype.

!!! warning "Live documentation" 
    - This documentation has been generated along the development process, therefore is no curated material. If some parts don't make sense refer to the code in the public repos.


## Prototype architecture

The previous version of the prototype implemented a different architecture, explained in detail in the article [Task assignment in Amara. Prototyping Round Robin with blockchain (I)](https://p2pmodels.eu/task-assignment-in-amara-prototype-round-robin/). In this new version of the protoype the architecture has been simplified.

<img src="/assets/images/architecture.jpg" alt="Architecture">

At the frontend level the web app has been extended adding several views:

- Configuration view: allows the admin to configure a URL that can be shared with the user so that the correct user and model are set for the test.

- User view: this view employs URL parameters to configure the model used. A new model has been introduced, the round robin + calendar, which lets the user set an availability calendar so the algorithm considers it when assigning new tasks.

- Admin view: the new admin view lets the admin manage all the models, one at a time, providing a user-friendly interface that simplifies all actions: restarting the prototype and starting and stopping the manager. Several information tables have been added so that the state of the process is easier to track.

At the back-end level, the task manager server has been removed, now the client app (in the admin view) manages the reallocation of tasks using timeouts instead of cron jobs. Therefore, a tab with the admin view has to be opened when the prototype is being used. The main reason for this change is to ease the experimentation process allowing our team to set up the test environment in a few clicks (rather than connecting to a server and running the manager-script and other operations that require technical knowledge).

Moreover, Aragon has been removed from the stack. Therefore, the underlying DAO that used to operate the task allocation app has been removed. Now each model consists of an independent smart contract and a subgraph that keeps track of the current state of each instance thus reducing inner complexity to achieve similar results.

Finally, at the blockchain level, the only changes introduced have been the creation of the new model alongside the tests of most features.

## Technology stack

Below is a diagram featuring the technologies used in the development of this prototype:

<img src="/assets/images/stack.jpg" alt="Technology stack">

## Get started - development local environment

In order to set up a local environment for the protoype (connected to the Goerli network) you only need to set up a local server with the client app:

- Task allocation frontend: at least two clients have to be active at the same time. One in the admin view (/admin) which will start and stop the tasks manager. And a second one in a user view, whici will be able to accept tasks, reject them... depending on the selected model.

```bash

git clone https://github.com/p2pmodels/task-allocation-frontend
cd task-allocation-frontend
npm install
npm start

```

- Task allocation prototype: a repo containing the smart contracts (smart-contracts folder) and subgraphs (subgraphs folder) for each model. It uses hardhat for local testing and testnet deployment of the smart contracts and The Graph protocol to create the subgraphs to track the smart contract events and process the information to be requested by the client app.

```bash

git clone https://github.com/p2pmodels/task-allocation-prototype

```

In case you have any errors installing dependencies try cleaning up the cache.

## License

This prototype is licensed under [GNU General Public License v3.0](https://www.gnu.org/licenses/gpl-3.0.en.html)
