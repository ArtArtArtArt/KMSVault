# Spinlock

Spinlock ???

Is a primitive which while blocking the thread does not put it to sleep, but makes it poll the lock again and again. Putting thread to sleep and then waking it up may be very costly operation if the actiual time that is spend inside the clock is low.
Moreover spinlock is unnescesary on a single core system (???)

Propgrammer cannot be sure if he will be benefitting from spinlock from the get go.

Modern systems have hybrid apporaches.
For exampl a hybrid mutex will not put the thread to sleep immediately, it will ask thread to poll him several times before doing so.

Hubrid spinlock behaves like a spinlock but might stop thread entirely after some time. called yeillding. 

If in doubt - use mutexes, they are usually spinlocking for some time.



https://getpocket.com/read/137289797

#interview #networking #programming 