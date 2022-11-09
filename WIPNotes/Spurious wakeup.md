# Spurious wakeup
Spurious wakeup - when a conditional variable is notified, but between the notification sent and awakening another thread has entered and changed the condition back.
The condition should be checked again on cond var wait in order to prevent the spurious wakeup.


---
status: #🌱
tags: #programming/multithreading  
related: 