# **Round robin (RR)**

In this model the users have a feed of _assigned_ tasks. Tasks are assigned to one user at a time for a short period of timehe first user to successfully send a confirmation transaction will get the tasks assigned. Therefore there will be a lot of transactions that will resolve as error when a late request arrives. Once a tasks has been assigned to the user the feed is hidden and only the assigned task is shown.

## User workflow

<div class="grid-2col">
    <div>
        <img src="/assets/images/rr-user-view-1.png" alt="User empty feed view">
        <p class="ta-center">User empty feed view</p>
    </div>
    <div>
        <img src="/assets/images/rr-user-view-2.png" alt="User feed view">
        <p class="ta-center">User feed view</p>
    </div>
    <div>
        <img src="/assets/images/rr-user-view-3.png" alt="User accept task pop up">
        <p class="ta-center">User clicks the accept task button, a dialog pops up</p>
    </div>
    <div>
        <img src="/assets/images/rr-user-view-4.png" alt="User confirm transaction">
        <p class="ta-center">User clicks on create transaction button, Metamask pops up</p>
    </div>
    <div>
        <img src="/assets/images/rr-user-view-5.png" alt="User view transaction sent">
        <p class="ta-center"> Transaction is sent, tasks get disabled</p>
    </div>
    <div>
        <img src="/assets/images/rr-user-view-6.png" alt="User view task accepted">
        <p class="ta-center">Only the task accepted is shown</p>
    </div>
</div>

## Admin view

<div class="grid-2col">
    <div>
        <img src="/assets/images/rr-admin-view-1.png" alt="Admin view manager stopped">
        <p class="ta-center">The task manager is stopped, no tasks get assigned to users</p>
    </div>
    <div>
        <img src="/assets/images/rr-admin-view-2.png" alt="Admin view manager started">
        <p class="ta-center">Admin starts the task manager</p>
    </div>
    <div>
        <img src="/assets/images/rr-admin-view-3.png" alt="Admin view task assigned">
        <p class="ta-center">Task get assigned to a user</p>
    </div>
    <div>
        <img src="/assets/images/rr-admin-view-4.png" alt="Admin view multiple tasks assigned">
        <p class="ta-center">More tasks are assigned</p>
    </div>
    <div>
        <img src="/assets/images/rr-admin-view-5.png" alt="Admin view task accepted">
        <p class="ta-center">User 3 accepts a task</p>
    </div>
</div>
