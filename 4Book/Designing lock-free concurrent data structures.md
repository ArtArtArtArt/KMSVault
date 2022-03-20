


























# Designing lock-free concurrent data structures

^1b650b

p.204

using atomic to create a spinlock
```cpp
class spinlock_mutex 
{
	std::atomic_flag flag; 
public: 
	spinlock_mutex(): flag(ATOMIC_FLAG_INIT) {}
	void lock() 
	{
		while(flag.test_and_set(std::memory_order_acquire));
	} 
	
	void unlock() 
	{ 
		flag.clear(std::memory_order_release); 
	} 
};
```
it is a `non-blocking` implementation (no thread is blocked (suspended)) but it is non `lock-free` (atomic flag is effectively a lock)

`lock-free` means that more then one thread is able to access the data structure concurrently. It might be achieved by sometimes redoing what was already done due to the fact that another thread might have broken something in the meantime. So **if any other thread is suspended by the system the remaining threads will be able to finish the job - this is not possible with the spinlock for example.**
This algorithms are prone to [[thread starvation]]. Due to redoing some threads might not be able to progress at all, or very slowly, if they are not lucky.

`wait-free` means that any thread can achieve it's goal in some bounded number of threads disregarding what other threads do.


[[hazard pointer]] - tmp ptr that is used to point to a resources that is used by some other thread and only when we know that resource is not used then we remove it.
[[reclaim function]] - ???

[[memory ordering]] - 

[[Guideline for writing lock-free data structures]] (p.244)

--- 
status: #⚙️ 
tags:
related: [[c++ concurrency in action BOOK]]