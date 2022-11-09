# Garbage collector in unreal
**find info on this**

read here
https://docs.unrealengine.com/4.27/en-US/ProgrammingAndScripting/ProgrammingWithCPP/UnrealArchitecture/Objects/Optimizations/

also remind yourself on main concepts of the engine

GC maintains graph of ownership and searches for orphans
Any object can be added to root and thus will not be destroyed
Implicit call to a destroy function just marks an object for destroy.

--- 
status: #🌱
tags: #job_tasks  
related: 