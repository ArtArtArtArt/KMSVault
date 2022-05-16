# read/write, cv wait mutex, bounded buffer
https://www.youtube.com/watch?v=7zI_4CKk-3Y&ab_channel=ChrisKanich

Read/Write locks and bounded buffers

You should not write while anyone is reading. 
Two different writers should not enter.

If you want to lock for reading you have to count number of readers (in a critical section). This counter increases with added reader and decreases with removed reader. Only on counter equals zero then writers will be allowed.

Bounded buffer is used for producer/consumer situation.

wait needs a mutex which is locked, because it will release it and reacquire the lock.

Additional check of the condition should be made.



---
status: #⚙️ 
tags: #programming/multithreading 
related: 