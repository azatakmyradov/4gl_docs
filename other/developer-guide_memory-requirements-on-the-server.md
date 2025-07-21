[Index](index.html)  [Home](getting-started_home.html)

Memory requirements on the server

## Memory management on the process server

The Adonix process that executes the Sage X3 code on the server manages two segments of memory to handle the resources it has access to.

* The main memory manages all local and global variables, all table buffers, and all mask buffers (when using version 6 style programming). All variables stored in [L], [V], [F], and [M] variable classes are affected.
* The heap memory manages all class instances created with the [NewInstance](4gl_newinstance.html) instruction and released by the [FreeInstance](4gl_freeinstance.html) and [FreeGroup](4gl_freegroup.html) instructions.

## Available variables

Two variables exist that define the maximum size allowed to a process for each segment: [maxmem](4gl_maxmem.html) and [maxheap](4gl_maxheap.html). Assigning a given value to each does not imply that the process will use the whole amount of memory immediately. The process will allocate the memory without exceeding the fixed limits.

## How to dimension these variables

Set these variable values in the **GESADS** function's folder record. Indeed, modifications done in **GESADS** overwrite content in **APL.ini**. To access **GESADS**, go to **Setup > General parameters > Folders**.

You can also define these default values for these two variables in the **APL.ini** configuration file, which contains assignments of variables used by the engine when a session starts. Reassignment can be done at any time in a script.

A measure of the remaining memory of every type is given by the two functions [freemem](4gl_freemem.html) and [freeheap](4gl_freeheap.html).

If the required memory to manage the buffer exceeds the limit, an error (more memory available) will appear. You should measure the memory consumption in the scripts handling the biggest resource size, to be sure that this error will not appear at execution time.

* The main memory can be filled with big masks (having large grids), big arrays, BLOBS, or CLOBS, especially if the variables are global (local variables are released at `End` execution). The `Kill` and `Close Mask` instructions can be used to release the main memory.
* The heap memory is only filled with instances. [FreeInstance](4gl_freeinstance.html) releases this type of memory and can be used with groups to ease memory management. The [Heapdmp](4gl_heapdmp.html) function can be used to check which are the instances stored at a given point in the heap memory.

The amount of memory managed by **maxmem** and **maxheap** is not used immediately by the process. It is the upper limit of memory consumption managed by a process.

Every parameter can be set up independently:

* [maxmem](4gl_maxmem.html) by taking into account the biggest quantity of memory spent by a Classic session.
* [maxheap](4gl_maxheap.html) by taking into account the biggest quantity of memory spent by a Version 7 native session connected on a Sage X3 server (a Classic page or a Version 7 native function using Sage X3 entities).

## Database buffers

The **sadora** or **sadoss** processes that handle the database connection use the value of variable [sadmem](4gl_sadmem.html) to dimension buffers. The value of this variable can be defined in **GESADS** or the **APL.ini** configuration file. A reassignment cannot be done dynamically in a script.

**Note**: **sadora** is for Oracle and **sadoss** is for SQL Server.

  

[Index](index.html)  [Home](getting-started_home.html)