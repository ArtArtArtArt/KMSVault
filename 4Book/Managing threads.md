



























# Managing threads

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
 ```

### Picking number of threads in a runtime

```cpp
std::thread::hardware_concurrency()
```

--- 
status: #🌲
tags:
related: [[BOOK c++ concurrency in action]]