
-----
###### This chapter combines three of the most common initial steps in an investigation, determine what is running, what their doing, and what security context

### Processes
----
At the center of a process is the `_EPROCESS`, which is the name of the structure allocated in the kernel pool that windows uses to represent a process.

Although names may differ, this is a fundamental part of all operating systems. 

Each process has its own private virtual memory space that's isolated from other processes to avoid confliction. Inside this space you can find the process executable; loaded DLLs, stacks, heaps and allocated memory regions
![[Pasted image 20250526042827.png]]

As the image shows, each `_EPROCESS` points to a variety of things including `security identifiers and privilege data`. That information is one of the key ways the kernel enforces security and access control.

##### Data Structures
Windows tracks processes by assigning them a unique `_EPROCESS` structure that resides in a non-paged pool of kernel memory. It looks like the following

![[Pasted image 20250526043226.png]]

### Process Organization
----
The `_EPROCESS` structure contains a `_LIST_ENTRY` structure called `ActiveProcessLinks`. This inherited structure contains two values, a backwards link `blink` and forwards link `flink`. This acts as an doubly linked-list and allows for all the processes to be chained together.

Tools such as task-manager and process explorer rely on walking the linked list to find processes

### Enumerating Processes in Memory
----
When volatility attempts to list processes, it will access the `_KDDEBUGGER_DATA64` data block, from there it will access the `PsActiveProcessHead` member, which points to the head of the double-linked list of `_EPROCESS` structures.

This is not the only way to find the start of processes, and that is important as the linked-list pointers, pool tags, and the debugger data block are non-essential and can be removed to defeat forensics tools

### Analyzing Process Activity
---------
Volatility provides a few commands to extract information about processes:
- pslist - walks the linked list
- pstree - walks the linked list but displays in tree format
- psscan - scan for objects instead of relying on linked list
- psxview - locates processes using `alernate process listings`