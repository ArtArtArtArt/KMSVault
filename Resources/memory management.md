---
tags: 
 - resource
---


https://getpocket.com/read/575080653
https://isocpp.org/wiki/faq/freestore-mgmt?utm_source=pocket_mylist

The best way to fight the memory leaks are smart pointers and containers (if you are working with multiple objects)



## Is it safe to delete the same pointer twice?
 - no! It may lead to many kinds of unintentional changes

## Free allocated with  new and delete allocated with malloc
 - no! it is not fact that these functions will be on the same [[heap]]


## Why should I null deleted pointer
To protect against double delete. Delete on nullptr is safe.

## Garbage collector types
[[Conservative garbage collectors]]
[[Hybrid garbage collectors]]

