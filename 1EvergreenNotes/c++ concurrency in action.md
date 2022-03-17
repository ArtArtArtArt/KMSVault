---
status: 🌱
type:
 - MOC
 - book outline
---


# c++ concurrency in action


## 1. Hello, world of concurrency in C++

Main reasons to use [[concurrency]]
 - separation of concerns
 - performance


## 2. Managing threads
p 41

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

p. 129