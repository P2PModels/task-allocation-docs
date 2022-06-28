

# Calendar 

## FullCalendar

After trying different Calendar libraries, the winner was FullCalendar. It was the most simple to install and test, and it is very customizable. 

In the principal screen, there is a button that you can click in order to view the availability calendar. After doing this, a pop up with the calendar appears. 

In the Calendar component we decided to make the following customizations:

- First view is the week view (with hours: timeGridWeek) (without hours: dayGridWeek)

- When selecting a part of the calendar, it asks you to enter the name of the event (selectClick)

- When selecting a part of the calendar at the same tme that we press alt, we can also add a function (selectClickAux)

- Header tool bar with components that we choose

- A value of true in selectMirror will draw a “placeholder” event while the user is dragging (similar to what Google Calendar does)

- We change the color and border of the events to be similar to the inVision ones

- We only show month and week, to show day add timeGridDay in the headerToolbar property

- To emphasize in grey the time before today, we try to use eventDrop