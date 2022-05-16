# Subclass sandbox pattern
https://gameprogrammingpatterns.com/subclass-sandbox.html?utm_source=pocket_mylist

add protected methods in a base class for each atomic "query" to different subsystems. Useful when programming subclasses that will use many different subclasses. Any of these protected methods are used in a virtual Activate() method. 

Here is another good reason to use inheritance - to restrict usage of some methods.


---
status: #🌱
tags: #gamedev/patterns 
related: 