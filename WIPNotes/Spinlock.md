
Is a primitive which while blocking the thread does not put it to sleep, but makes it poll the lock again and again. Putting thread to sleep and then waking it up may be very costly operation if the actual time that is spend inside the clock is low.
Moreover spinlock is unnecessary on a single core system (???)

Programmer cannot be sure if he will be benefitting from spinlock from the get go.

Modern systems have hybrid approaches.
For example a hybrid mutex will not put the thread to sleep immediately, it will ask thread to poll him several times before doing so.

Hybrid spinlock behaves like a spinlock but might stop thread entirely after some time. called yielding. 

If in doubt - use mutexes, they are usually spin locking for some time.

https://getpocket.com/read/137289797

 
---
status: #⚙️ 
tags: #interview #networking #programming 
related: 

