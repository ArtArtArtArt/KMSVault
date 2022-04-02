---
status: 🌱
---
# docker
#programming/devops 

https://www.youtube.com/watch?v=rOTqprHv1YE

what is docker

![[Pasted image 20220315083859.png]]

Number of apps for devops
![[Pasted image 20220315084143.png]]


Container is a software package that consists of all the dependencies required to run an app.

https://www.youtube.com/watch?v=-NzfOhSAZpA

![[Pasted image 20220315092210.png]]

Docker relies on Linux idea of [[Linux namespace|namespaces]]. Windows has to mimic it.

Examples of namespaces: 
 - files (mnt)
 - PIDs
 - Netword
 - IPC (interprocess communications, [[Linux pipes|pipes]])
 - Unix timesharing System (UTS) isolated host and domain names?
 - User ID. You can be a host to your process but not to your machine



Docker is written in GO language.

Do when you create a new process inside a docker you are setting new namespaces for this process. They are restricted so the process feels like running in a very special place.

When child process starts running it has all the namesapces copied to it beforehand by the parent process. But after it starts it sets a new root, we set the program as the only process visible to PIC, environmental variables might be set here and etc.

At the end of the day it all looks like we have a separate machine with only one process. But if you need more than one process there is a high chance that you need a virtual machine

All the instructions needed for the docker to run your app is called an image. It can be created from the docker file. 
Docker file has some commands and run command. Every time you call a run command a new layer of the image is created.

So docker may create a subsystem inside a subsystem easily.
