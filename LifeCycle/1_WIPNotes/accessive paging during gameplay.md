# accessive paging during gameplay
Active paging in Unreal Engine - what is the reason? Can it be fixed using code?


Page faults - hard, soft 
Hard - page not found on file or disk
Soft - page found somewhere


https://stackoverflow.com/questions/5684365/what-causes-page-faults


A page fault is a trap to the software raised by the hardware when a program accesses a page that is mapped in the virtual address space, but not loaded in physical memory.


There are soft page faults, where all the kernel needs to do is add a page to the [[working set of the process]].

Partially reasons for page fault
Reason for Fault

_Result_

Accessing a page that isn’t resident in memory but is on disk in a page file or a mapped file

_Allocate a physical page, and read the desired page from disk and into the relevant working set_

Accessing a page that is on the standby or modified list

_Transition the page to the relevant process, session, or system working set_

Accessing a demand-zero page

_Add a zero-filled page to the relevant working set_

Writing to a copy-on-write page

_Make process-private (or session-private) copy of page, and replace original in process or system working set_

![[Pasted image 20220613113027.png]]



My guess is that in the process, a lot of memory is being allocated, leading to demand-zero page faults

*What is demand zero page fault*
Demand Zero Faults/sec **The rate at which a zeroed page is required to satisfy the fault**. Zeroed pages are pages emptied of previously stored data and filled with zeros. These are a security feature of Windows that prevent processes from seeing data stored by earlier processes that used the memory space.



**Can [[Working set, Private Bytes, Virtual Bytes]] growth influence it???**


I found Page Fault monitor App which helped determine some specific code lines which led to page faulting

---
status: #🌱
tags: #job_tasks 
related: [[Virtual memory]]