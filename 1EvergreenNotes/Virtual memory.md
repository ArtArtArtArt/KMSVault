# Virtual memory
Virtual memory = unlim memory + protected
Protected mode
Segments
Page


https://www.youtube.com/watch?v=qcBIvnQt0Bw&list=PLiwt1iVUib9s2Uo5BeYmwkDFUh70fJPxX&ab_channel=DavidBlack-Schaffer

Three memory problems:
 - not enough RAM (legacy problem, now we have enough RAM usually, and if we do not virtual paging might slow it so much that it is not even worth doing)
 - holes in our address space (appear you run multiple programs and then you quit some of them) (memory fragmentation)
 - program writing over each other (two programs might want to write the exact same address by number)

What is virtual memory 
 - indirection (map program used address to the real one)
 - Page Tables and translation
 - Where do we store page tables
 - How we make them run fast?
 - Virtual memory and caches

https://www.youtube.com/watch?v=eSPFB-xF5iM&list=PLiwt1iVUib9s2Uo5BeYmwkDFUh70fJPxX&index=2&ab_channel=DavidBlack-Schaffer

https://www.youtube.com/watch?v=qlH4-oHnBb8&list=PLiwt1iVUib9s2Uo5BeYmwkDFUh70fJPxX&index=3&ab_channel=DavidBlack-Schaffer

Virtual memory takes program addresses and maps them to RAM addresses


Because of program isolation using virtual memory your processes now cannot share data, but we can use mapping to make processes share some data

![[Pasted image 20220613115913.png]]

https://www.youtube.com/watch?v=59rEMnKWoS4&list=PLiwt1iVUib9s2Uo5BeYmwkDFUh70fJPxX&index=4&ab_channel=DavidBlack-Schaffer


Physical memory == physical RAM
 
How does a program access memory?

![[Pasted image 20220613120158.png]]


![[Pasted image 20220613120249.png]]

https://www.youtube.com/watch?v=KNUJhZCQZ9c&list=PLiwt1iVUib9s2Uo5BeYmwkDFUh70fJPxX&index=5&ab_channel=DavidBlack-Schaffer

Pages are used for less entries in the translation table

![[Pasted image 20220613120536.png]]
![[Pasted image 20220613120648.png]]

https://www.youtube.com/watch?v=bShqyf-hDfg&list=PLiwt1iVUib9s2Uo5BeYmwkDFUh70fJPxX&index=8&ab_channel=DavidBlack-Schaffer


How do we know that the page is not in RAM?
Page Table Entry points to DISK
 
 - OS chooses a page to evict from RAM memory and write to disk
 - If the page is dirty it has to be written to disk first
 - OS reads the page and puts it into ram
 - updates table
 - goes back to instruction which caused the page foult

OS usually starts some other app while it is doing page manipulation - because it knows it will take so long
![[Pasted image 20220613122329.png]]

Page fault is the slowest possible thing that can happen to a computer

Specific ways to tackle it 
![[Pasted image 20220613122600.png]]
https://www.youtube.com/watch?v=uDzXXnNy544&list=PLiwt1iVUib9s2Uo5BeYmwkDFUh70fJPxX&index=9&ab_channel=DavidBlack-Schaffer

![[Pasted image 20220613122809.png]]






status: #⚙️ 
tags: #programming/os 
related: 