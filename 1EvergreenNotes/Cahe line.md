---
status: 🌾
---
# Cahe line
A modern CPU may have several cache lines. L1, L2, L3
They differ by size and access time.


# How much is loaded at a single time?

Modern PC fetch 64B of memory before the cache line boundary which is the largest memeory below the one you need is a multiple of 64.

Modern PC transfer 8 bytes at a time. So update of 64B is 8 transfers.

[](stackoverflow.com/questions/3928995/how-do-cache-lines-work)
[stackoverflow answer](https://stackoverflow.com/questions/3928995/how-do-cache-lines-work)


If we are using multiple processes then different cahces might be storing the same data. [[false sharing | False sharing]] might occur


#interview #programming/low_level