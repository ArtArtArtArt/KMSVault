---
status: ⚙️
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

## Avoiding data race

 - Protect data so only the thread which is making the change can see the intermediate stages which break the invariant
 - [[Lock free programming]] making sure that all changes are atomic and invariant is never broken. (more in chapters 5 and 7)
 - Doing the changes in a transaction privately and then try to commit the changes in one step. Also known as [[software transactional memory]]

	
	Stopped at : Protecting shared data with mutexes (p.60)



