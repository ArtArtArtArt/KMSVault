# Designing lock-based concurrent data structures

Using locks to create a concurrent data structures. (seems understandable)

WHY ARE CONDITIONAL VARIABLES USEFUL?
*Condition variable lock the unizue_lock(mutex) with the wait command. This lock will be freed only when notify_one/all is called elsewhere. Now we can separate the block and the condition to unlock to separate parts of the code. BUT WE CAN DO THE SAME WITH MUTEX??
The difference seem to be that cond_var is designed to be signaled from another thread.
And sometimes conditions are not met and some thread might be locking/unlocking the mutex unnesceserily. So the conditional varibale might be used here.
*

--- 
status: #⚙️ 
tags:
related: [[BOOK c++ concurrency in action]]