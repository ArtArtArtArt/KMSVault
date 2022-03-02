---
status: ⚙️
type: 
 - discussion
tags:
 - programming 
 - interview 
---

Conditional variable example of usage:

```cpp
#include <iostream>
#include <string>
#include <thread>
#include <mutex>
#include <condition_variable>
 
[std::mutex](http://en.cppreference.com/w/cpp/thread/mutex) m;
std::condition_variable cv;
[std::string](http://en.cppreference.com/w/cpp/string/basic_string) data;
bool ready = false;
bool processed = false;
 
void worker_thread()
{
    // Wait until main() sends data
    [std::unique_lock](http://en.cppreference.com/w/cpp/thread/unique_lock)<[std::mutex](http://en.cppreference.com/w/cpp/thread/mutex)> lk(m);
    cv.wait(lk, []{return ready;});
 
    // after the wait, we own the lock.
    [std::cout](http://en.cppreference.com/w/cpp/io/cout) << "Worker thread is processing data\n";
    data += " after processing";
 
    // Send data back to main()
    processed = true;
    [std::cout](http://en.cppreference.com/w/cpp/io/cout) << "Worker thread signals data processing completed\n";
 
    // Manual unlocking is done before notifying, to avoid waking up
    // the waiting thread only to block again (see notify_one for details)
    lk.unlock();
    cv.notify_one();
}
 
int main()
{
    [std::thread](http://en.cppreference.com/w/cpp/thread/thread) worker(worker_thread);
 
    data = "Example data";
    // send data to the worker thread
    {
        [std::lock_guard](http://en.cppreference.com/w/cpp/thread/lock_guard)<[std::mutex](http://en.cppreference.com/w/cpp/thread/mutex)> lk(m);
        ready = true;
        [std::cout](http://en.cppreference.com/w/cpp/io/cout) << "main() signals data ready for processing\n";
    }
    cv.notify_one();
 
    // wait for the worker
    {
        [std::unique_lock](http://en.cppreference.com/w/cpp/thread/unique_lock)<[std::mutex](http://en.cppreference.com/w/cpp/thread/mutex)> lk(m);
        cv.wait(lk, []{return processed;});
    }
    [std::cout](http://en.cppreference.com/w/cpp/io/cout) << "Back in main(), data = " << data << '\n';
 
    worker.join();
}
```