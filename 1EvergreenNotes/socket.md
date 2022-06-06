# socket
of a connection. There is a server and a client socket. Once a connection is established a communication between two may start.

There are two kinds of sockets:
 - TCP
 - DATAGRAM (UDP)

TCP provides reliability, IP provides routing

### TCP sockets

Initialize TCP socket connection:
```cpp
SOCKET sock_X = socket(AF_INET, SOCK_STREAM, NULL);
```

Send data with TCP socket:
```cpp
answer = send(sock_X, "You have connected to SERVER", 46, NULL);
```

Receive data with TCP socket:
```cpp
answer = recv(sock_X, MESSAGE, sizeof(MESSAGE), NULL);
```

### UDP sockets

Initialize UDP socket connection:
```cpp
SOCKET sock_X = socket(AF_INET, SOCK_DGRAM, NULL);
```

Send data with UDP socket:
```cpp
answer = sendto(sock_X, "Welcome to SERVER", 46, 0, (struct sockaddr *)&ADDRESS, sizeof(ADDRESS));
````

Recieve data with UDP socket:
```cpp
answer = recvfrom(sock_X, MESSAGE, sizeof(MESSAGE), 0, (struct sockaddr *)&ADDRESS, sizeof(ADDRESS));
```
[[Strategies of implementation a socket oriented server]]

status: #🌱
tags: #programming/network 
related: [[130 Network concepts MOC]]