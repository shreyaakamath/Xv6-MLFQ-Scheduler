Overview
----------------------
Build an MLFQ scheduler with four priority queues; the top queue (numbered 0) has the highest priority and the bottom queue (numbered 3) has the lowest priority. When a process uses up its time-slice, it should be downgraded to the next (lower) priority level. The time-slices for higher priorities will be shorter than lower priorities.


Objectives
----------------
There are two objectives to this assignment:

To familiarize yourself with the details of a MLFQ scheduler.
To show how process behavior (i.e., how long a process uses the CPU before performing I/O or sleeping) interacts with the scheduler by creating an interesting timeline graph.
Overview

In this project, you'll be implementing a simplified multi-level feedback queue (MLFQ) scheduler in xv6.

The basic idea is simple. Build an MLFQ scheduler with four priority queues; the top queue (numbered 0) has the highest priority and the bottom queue (numbered 3) has the lowest priority. When a process uses up its time-slice, it should be downgraded to the next (lower) priority level. The time-slices for higher priorities will be shorter than lower priorities.

Details
---------------
You have three specific tasks for this part of the project.

1)Implement MLFQ: Your MLFQ scheduler will be very simple and will not have any mechanisms to prevent gaming or starvation. Specifically, your MLFQ scheduler should follow these very precise rules:

When a process is first created, it should be placed at the highest priority. Place this process at the end of the high priority queue.
At any given point in time, the highest-priority ready process should be run.
The time-slice for priority 0 should be 1 timer tick. The times-slice for priority 1 is 2 timer ticks; for priority 2, it is 4 timer ticks; for priority 3, it is 8 timer ticks.
When a timer tick occurs, whichever process was currently using the CPU should be considered to have used up a timer tick's worth of CPU. (Yes, a process could game the scheduler this way by relinquishing the CPU just before the timer tick occurs; ignore this!)
If a process wakes up after voluntarily relinquishing the CPU (by performing I/O or sleeping), it should be placed at the front of its queue; it should not preempt a process at the same priority.
Whenever a process is moved to a different priority level, it should be placed at the end of the corresponding queue.
A round-robin scheduler should be used for processes at the lowest priority.
There is no mechanism for the priority of a process to be raised again. (Yes, a process could starve and never recieve any CPU if higher-priority processes keep arriving; ignore this!)

2)Create getpinfo(): You'll need one new system call for this project: int getpinfo(struct pstat *) . This routine returns some basic information about each process: its process ID, how many times it has been chosen to run, and which queue it is currently on (0, 1, 2, or 3). To do this, you will need to fill in the pstat structure as defined here: here. Do not change the names of the fields in pstat.h

3)Make a graph: You should make a graph that shows some timelines of processes running with your scheduler, including which queue each process is on, and how much CPU they received. To obtain the info for your graph, you should use the getpinfo() system call. Make up a workload (or set of workloads) that vary how long each process uses the CPU before voluntarily relinquishing the CPU (e.g., by calling sleep()). Think about what types of workloads will show interesting and useful results. Use the graphs to prove to us that your scheduler is working as desired.
