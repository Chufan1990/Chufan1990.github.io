---
layout: post
title: C/C++ Socket
date: 2017-10-31
categories: blog
tags: [Linux, C++, Socket]
description: C/C++ Socket FAQ and How-to Win+Linux
---

## What are sockets?

Well sockets are used as an interface to access a network through your operating system. Imagine your system to be contained inside of a locked room, with the only piont of entry being a wall totally plastered in wall plugs. You create a socket, bind it to the plug and you've got access outside on the network. Also while we're at it, you can think of your firewall as a dude that stands about watching the wall plugs pulling out ones that it doesn't like XD.

## Getting Started

First you'll need to include the appropriate header files for sockets.

<u>Windows</u>

```cpp
#include <winsock.h>
```

Pass this to GCC: /lib/libws2_32.a
winsock as in Windows Socket

<u>Linux</u>

```cpp
#include <sys/type.h>
#include <sys/socket.h>
#include <netinet/in.h>
#include <arpa/inet.h>
```

Pass these to GCC: -lsocket lnsl
The headers for Unix are split up more so you don't get the overhead of a huge amount of stuff you just don't need!

<u>Extra studd for windows..</u>
You'll need a load of extra stuff for Windows：

```cpp
WSADATA wsaData;
WSAStartup(0x0202, &wsaData);
```

The first line is adata structure that holds data about the current winsock version. The second line initializes the winsock component so you can use it. MISS THESE LINES AND NONE OF THIS WILL WORK.

<u>Creating your first socket</u>
First you need to define some information about the type of connection you want to establish. Here I'm after a two-way socket (SOCK_STREAM) that uses IPv4 (AF_INET) and uses TCP(IPPROTO_TCP) for reliable data transfer. Thanksfully both ways are interoperable between OS's.

```cpp
int mySocket;
struct sockaddr_in address;

address.sin_family = AF_INET;
if((thisSocket = socket(AF_INET, SOCK_STREAM, IPPROTO_TCP)) < 0){
	perror("\nSocket Creation FAILED!"); 
	return -1;
}
```

<u>Closing your first socket</u>
The difference here come from the way both OS's handle networking..

<u>Windows</u>

```cpp
closesocket(mySocket);
WSACleanup();
```

<u>Linux</u>

```cpp
close(mySocket);
```
## Hosting a connection with your socket
There are three stages to host and establish a connection:

1. Bind the 