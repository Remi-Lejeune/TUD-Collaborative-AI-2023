# Agent explanation
_What is this doc:_ Explains the logic inside the decide_on_actions inside the
Official Agent.

## The Main loop
The agent loops until termination. It switches between different passes, which
dictate which actions where taken
Phases will be sub sections, and detail their transitions and someof the checks

### Find next goal:
Sets remaining zones, remaining victims
CH#ecks remaining victims, if we already have seen them
If their exact location is known, we plan a pace =>  **Path to victim** 

If human has seen victim (room is known, location is not) => **Path to room**

If no victims have been seen yet, pick unsearched rooms => **Pick Unselected
Room**


### Pick unsearched room
Identify unexplored/ start search again: **Path to room**

### Follow path to room
If human finds target victim first => **Find next goal**

If human already searched target with no victims => **Find next goal**

If arrived at door => **Remove_obstacle_if_needed**

### Remove Remove_obstacle_if_needed
Repetition of code blocks for each obstacle type, differences to be
investigated

If negative human response => **Find next goal**

If positive => **Wait for human indefinitely**

When human arrive, remove obstacle && no obstacle => **Enter room**

### Enter Room
If human rescued target **Find next Goal**
If target elsewhere **Find next Goal** (needs investigating)
If human already searched area **Find next Goal**
Else **Room search path**

### Room search path
=> **Follow room search path**

### Follow search room path
identify victims:
If victim which has already been found, **Find next goal**
If victim found, message human **_wait indefinitely_**

### Plan path to victim

Plans path to goal => **Follow path to victim**

### Follow path to victim
If human interrupts => **Find next goal**

else => Take victim

### Take victim:
If human interrupts => **Find next goal**
Else **Plan path to victim => Follow path to droppoint => drop victim => find next**

## Other

### Process message (_processMessages)

This function is made to process messages from the human.
We could add our trust factor here instead of the main loop.

if received "search" 
    add room to list of room searched

if received "found" 
    add victim to found victim
    add room to list of room searched
    if human weak help them
    else add to "to do list"

if received "Collect"
    add victim to list of rescued victim
    add room to list of room searched
    if human weak help them

if received "Remove"
    agent comes to help remove the obstacle
    

### Send message (_sendMessage)
This is the function from which the agent sends message. It could be modified for debug purposes.

### Trust Belief
This function is where we need to implement the logic to compute the trust and eagerness.
Right now it adds + 0.1 of trust when a victim is rescued.

### Load Belief
This function is made load our "belief" (right now it only the trust value)