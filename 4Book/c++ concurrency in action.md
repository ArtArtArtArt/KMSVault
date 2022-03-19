
# c++ concurrency in action


## 1. Hello, world of concurrency in C++

Main reasons to use [[concurrency]]
 - separation of concerns
 - performance


## 2. Managing threads

### Joining threads
joinable - is a function that checks if we have already called join on a thread.
You should be careful with join if exceptions are are thrown.
Thread Guard might be used for this:

```cpp
class thread_guard
{
 std::thread& t;
	
public:
 explicit thread_guard(std::thread& t_):
 t(t_)
 {}
	
 ~thread_guard()
 {
 	 if(t.joinable())
	 {
		t.join();
	 }
 }
 thread_guard(thread_guard const&)=delete;
 thread_guard& operator=(thread_guard const&)=delete;
};
struct func;
void f()
{
	 int some_local_state=0;
	 func my_func(some_local_state);
	 std::thread t(my_func);
	 thread_guard g(t);
	 do_something_in_current_thread();
} 
```


Detached threads are often called daemon thread.

### Wait for each thread to finish
```cpp
std::for_each(threads.begin(),threads.end(),
			  std::mem_fn(&std::thread::join));
```

### Picking number of threads in a runtime

```cpp
std::thread::hardware_concurrency()
```

## 3. Managing data between threads

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


## Synchronizing concurrent operations

### [[Conditional variable]] 
wait function needs a lock as a parameter

```cpp
while (!stop_waiting()) {
    wait(lock);
}
```

wait need a lock to protect the conditional variable itself

### Future
[[std::async]] calls a function in a separate thread.
[[future]].get - block until get the result

[[future]].wait - block until result is available

#### Package task with future
[[std::package_task]]

*Creating tasks may be very important because specific threads should do specific tasks. So you separate task creation and task execution. Now you are able to implement separate policies for them.*

Package task is a wrapper over the callable, it can be called async and it can store the result or exception inside.


#### Promise and future

![[Pasted image 20220315132947.png]]


Using future and promise to communicate between threads.

*packaged_task vs promise/future:
is the same but packaged_task also has an associated function which will produce the result.*

If promise was destroyed without setting the value, an exception is stored there.

*async - is async call, might be or might not create a separate thread for this*


use std::shared_future if you need to wait for the future in different threads, otherwise a data race


Conditional variables may wait_until with timeout.


## The C++ memory model and operations on atomic types

С++11 Has a mutlithreaded aware memory model.

One of the gals of the Standarts Commitee is that there is no need for a lower-level language than C++.

Modification order - ???

### Atomic

```cpp
<atomic>
```

header contains standart atomic types.
is_lock_free() - tells if this types is using an atomic operation or "hidden" mutex.
atomic_flag does not have is_lock_free() function

atomic_flag::set_and_test().
```cpp
// spinLock.cpp

#include <atomic>
#include <thread>

class Spinlock{
  std::atomic_flag flag;
public:
  Spinlock(): flag(ATOMIC_FLAG_INIT) {}

  void lock(){
    while( flag.test_and_set() );
  }

  void unlock(){
    flag.clear();
  }
};

Spinlock spin;

void workOnResource(){
  spin.lock();
  // shared resource
  spin.unlock();
}

int main(){

  std::thread t(workOnResource);
  std::thread t2(workOnResource);

  t.join();
  t2.join();

}
```

	1.the first thread will set value to true (it will be possible because it is false by default)
	2.next thread will not be able to set this value because the value is true. It does not have an opportunity to set the value to false so it will wait untill the first thread uses clear


```cpp 
std::atomic<bool> 
```
can be copy constructable from a simple bool so it may have true as an initial value.

### compare_and_swap (CAS)
compare_exchange_weak - 
compare_exchange_strong - 
atomically compares and exchanges.

if the value == the first parameter then assign second parameter (and return true)
otherwisthe assign value to first parameter and assign false

good usage is (https://en.cppreference.com/w/cpp/atomic/atomic/compare_exchange)

```cpp
new_node->next = head.load(std::memory_order_relaxed);

//here other thread might have done something 
//to new_node->next
													   
while(!head.compare_exchange_weak(new_node->next, 
								  new_node, 
								  std::memory_order_release,
								  std::memory_order_relaxed))
```
Try it insert the new_node and if some other thread has done it then insert your value and try to insert head again.

 
all use memcopy functions.

**These compare exchange finctions are a cornerstone of programming with atomic types**.

weak may fail (because of spurious failure), strong retries if it fails. That is why weak is often used inside a loop and strong is not.

Spurious failure is fail not because values are not equal, but because of context switch, reloading of the same address in a cacheline etc, modification might fail failed. This might happen on some platforms where the "atomicness" of this operation is not guaranteed.

#### Usecases of CAS:
1. Adding an item to a linked list. Each thread

	1.  loads a **head ptr**
	2. creates a **new node**, 
		- `head might be changed here by another thread`
	3. tries to add **new node** to **head ptr**.
		- `will retry if head ptr is different, will assign a new head before the retry` 
	4. tries to swap the **head ptr** with the **new node**.

2. Implementing a spinlock based on `atomic_bool`
```cpp
bool criticalSection_tryEnter(lock)
{
  bool flag = false;
  return lock.compare_exchange_strong(flag, true);
}
```
compare_exchange_weak is not suitable here because it may fail due to [[spurious failure]] and a situation when no thread is occupying the critical section is likely.

3. You want and atomic to be updated by any thread, but if it is not updated then you try again (trigger for a state machine). 
```cpp
expected = false;
// !expected: if expected is set to true by another thread, done!
// Otherwise, it fails spuriously and we should try again.
while (!current.compare_exchange_weak(expected, true)
       && !expected);
```


## 6. Designing lock-based concurrent data structures

Using locks to create a concurrent data structures. (seems understandable)

WHY ARE CONDITIONAL VARIABLES USEFUL?
*Condition variable lock the unizue_lock(mutex) with the wait command. This lock will be freed only when notify_one/all is called elsewhere. Now we can separate the block and the condition to unlock to separate parts of the code. BUT WE CAN DO THE SAME WITH MUTEX??
The difference seem to be that cond_var is designed to be signaled from another thread.
And sometimes conditions are not met and some thread might be locking/unlocking the mutex unnesceserily. So the conditional varibale might be used here.
*

## 7. Designing lock-free concurrent data structures

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

## 8. Designing concurrent code

p.257