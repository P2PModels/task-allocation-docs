# __Task Allocation prototype__


## Introduction

At P2PModels we are implementing a new version of the Task Allocation prototype, to remove Aragon from the stack and implement new features such as a calendar to let the users select their working hours so that the algorithm takes them into account when assigning tasks. 

## Prototype architecture

The previous version of the prototype implemented the following architecture (from the article [Task assignment in Amara. Prototyping Round Robin with blockchain (I)](https://p2pmodels.eu/task-assignment-in-amara-prototype-round-robin/)):

<img src="/assets/images/architecture.jpg" alt="Architecture">

Some changes are being introduced, we'll comment them through the description of the previous architecture:

"At the blockchain level we find the Round Robin smart contract, which will serve as the application contract and will inherit from Base Task Allocation. The task of this contract is to abstract common characteristics of all contracts that implement task assignment models, whether permissions, events, status variables, etc.

As with the previous prototype, we will use a database to store the Amara demo accounts and a server that will act as API proxy to connect to the Amara API and obtain information related to the tasks stored in the smart contract.

We will also use a second server, corresponding to the Transaction Manager component, that will be in charge of reassigning the tasks once their allotted time period has lapsed. This will be done through cron jobs, which will be run by sending a transaction to the contract whenever a task’s allocatted period of time is up, thereby reassigning the task to a new user. The server will listen to contract events that are issued when a new job is created in order to then prepare a cron job.

The idea behind this component is to cover the costs related to these transactions. We want to spare the users (linguists) this expense, as it could severely affect the user experience and usability of the prototype. For the time being, costs will be assumed by a P2P Models Ethereum account, but in the future, an Amara account could be used to handle expenses. Another solution could be a multi-signature account controlled by the linguists themselves.

In order to connect with the smart contracts, we will use ~~the Round Robin Connector, developed specifically for the prototype using Aragon Connect~~ The Graph and Ethers library to directly connect to the Ethereum blockchain." 



## Technology stack

Below is a diagram featuring the technologies used in the development of this prototype:

<img src="/assets/images/stack.jpg" alt="Technology stack">

The stack is actually being updated. Aragon its being removed to simplify the architecture since the DAO was not being used.


## Get started - development local environment

In order to set up a local environment for the protoype (connected to the Rinkeby network) you need to set up the following services:

- Ethers manager: its a containerized service to handle the task allocation actions. It reallocates the task to the proper user and updates state variable on events from the smart contract.

``` bash

git clone https://github.com/p2pmodels/ether-manager 
cd ether-manager
docker container build . -t ether-manager:latest
docker run ether-manager:latest

```


- Front end: React app.

``` bash

git clone https://github.com/p2pmodels/task-allocation-frontend 
cd task-allocation-frontend
npm install
npm start

```
In case you have any errors installing dependencies try cleaning up the cache.


## License

This prototype is licensed under [GNU General Public License v3.0](https://www.gnu.org/licenses/gpl-3.0.en.html)





