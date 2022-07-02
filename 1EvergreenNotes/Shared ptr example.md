# Shared ptr example
Control block consists of 
 - shared ptr counter (which is atomic)
 - weak ptr counter (which is atomic)
 - deleter (for control block)
 - allocator (for control block)

Example op usage:
texture that is used by many threads and this texture should be released.




status: #🌱
tags: #interview #smart_pointer #programming/cpp 
related: 

