# **First Come First Serve (FCFS)**

In this model the users have a feed of _available_ tasks. The first user to successfully send a confirmation transaction will get the tasks assigned. Therefore there will be a lot of transactions that will resolve as error when a late request arrives. Once a tasks has been assigned to the user the feed is hidden and only the assigned task is shown.

## User workflow

<div class="grid-2col">
    <div>
        <img src="/assets/images/fcfs-user-view-1.png" alt="User feed view">
        <p class="ta-center">User feed</p>
    </div>
    <div>
        <img src="/assets/images/fcfs-user-view-2.png" alt="User accept task pop up">
        <p class="ta-center">User clicks the accept task button, a dialog pops up</p>
    </div>
    <div>
        <img src="/assets/images/fcfs-user-view-3.png" alt="User confirm transaction">
        <p class="ta-center">User clicks on create transaction button, Metamask pops up</p>
    </div>
    <div>
        <img src="/assets/images/fcfs-user-view-4.png" alt="User view transaction sent">
        <p class="ta-center">Transaction is sent, tasks get disabled</p>
    </div>
    <div>
        <img src="/assets/images/fcfs-user-view-5.png" alt="User view transaction confirmed">
        <p class="ta-center">Transaction is confirmed, The Graph is syncing behind scene</p>
    </div>
    <div>
        <img src="/assets/images/fcfs-user-view-6.png" alt="User view task accepted">
        <p class="ta-center">Only the task accepted is shown</p>
    </div>
</div>

## Admin view

<div class="grid-2col">
    <div>
        <img src="/assets/images/fcfs-admin-view-1.png" alt="Admin view task accepted">
        <p class="ta-center">Admin view is updated when a user accepts a task</p>
    </div>
</div>
