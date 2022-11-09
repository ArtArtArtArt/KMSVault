# Working set, Private Bytes, Virtual Bytes

**what is this?**
https://stackoverflow.com/questions/1984186/what-is-private-bytes-virtual-bytes-working-set

**Private Bytes** refer to the amount of memory that the process executable has _asked for_ - not necessarily the amount it is _actually using_. They are "private" because they (usually) exclude memory-mapped files (i.e. shared DLLs). But - here's the catch - they don't necessarily exclude memory _allocated by those files_. There is no way to tell whether a change in private bytes was due to the executable itself, or due to a linked library. Private bytes are also **not** exclusively physical memory; they can be paged to disk or in the standby page list (i.e. no longer in use, but not paged yet either).

**Working Set** refers to the total **physical** memory (RAM) used by the process. However, unlike private bytes, this also includes memory-mapped files and various other resources, so it's an even less accurate measurement than the private bytes. This is the same value that gets reported in Task Manager's "Mem Usage" and has been the source of endless amounts of confusion in recent years. Memory in the Working Set is "physical" in the sense that it can be addressed without a page fault; however, the standby page list is _also_ still physically in memory but not reported in the Working Set, and this is why you might see the "Mem Usage" suddenly drop when you minimize an application.

**Virtual Bytes** are the total **virtual address space** occupied by the entire process. This is like the working set, in the sense that it includes memory-mapped files (shared DLLs), but it also includes data in the standby list and data that has already been paged out and is sitting in a pagefile on disk somewhere. The total virtual bytes used by every process on a system under heavy load will add up to significantly more memory than the machine actually has.

So the relationships are:

-   Private Bytes are what your app has actually allocated, but include pagefile usage;
-   Working Set is the non-paged Private Bytes plus memory-mapped files;
-   Virtual Bytes are the Working Set plus paged Private Bytes and standby list.

**I do not understand a standby page, and some other stuff**

--- 
status: #🌱
tags: 
related: 