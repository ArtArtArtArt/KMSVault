




























# The C++ memory model and operations on atomic types
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

--- 
status: #⚙️ 
tags:
related: [[BOOK c++ concurrency in action]]