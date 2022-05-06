



























# Synchronizing concurrent operations
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

--- 
status: #⚙️ 
tags:
related: [[BOOK c++ concurrency in action]]