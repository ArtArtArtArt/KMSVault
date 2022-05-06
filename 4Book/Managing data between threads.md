# Managing data between threads

### Avoiding data race

 - Protect data so only the thread which is making the change can see the intermediate stages which break the invariant
 - [[Lock free programming]] making sure that all changes are atomic and invariant is never broken. (more in chapters 5 and 7)
 - Doing the changes in a transaction privately and then try to commit the changes in one step. Also known as [[software transactional memory]]

	
	Stopped at : Protecting shared data with mutexes (p.60)
### Mutexes
Stray pointers and references may render mutex ineffective. Never path them outside the ctirtical section.

### Interface problem
Some interfaces are just not suited for concurrency.
For example if stack has empty and size methods they cannot be relied on. The value is true at the time of the call but next instruction (which are for example inder if(empty)) may be harmful.

Solutions:
 - Share whole data structure. So any operations on it are atomic.

Top and pop become problematic - the solutions are on pages 68-70

### Deadlock
To avoid  deadlock lock mutexes in the same order.

std::lock can lock a number of mutexes in proper order. 

Also deadlock may appear for two threads when you call join on each other.

So the guideline is the following:
 - Avoid nested locks or at least acquire them in fixed order, hierarchy mutex also may help here (if we are not able to ensure that each thread acquires lock in the same order)
 - Avoid calling user code in locked sections
 - Avoid holding a lock while waiting for another thread
 

*Hierarchy mutex has a layer identifier and system dies not permit lock of the mutex of a higher layer if it already has locked mutex of a lower layer*

--- 
status: #⚙️ 
tags:
related: [[BOOK c++ concurrency in action]]