---
layout: post
title: C/C++ Socket
date: 2017-10-31
categories: blog
tags: [Linux, C++, Socket]
description: C/C++ Socket FAQ and How-to Win+Linux
---

#### What are sockets?

Well sockets are used as an interface to access a network through your operating system. Imagine your system to be contained inside of a locked room, with the only piont of entry being a wall totally plastered in wall plugs. You create a socket, bind it to the plug and you've got access outside on the network. Also while we're at it, you can think of your firewall as a dude that stands about watching the wall plugs pulling out ones that it doesn't like XD.

#### Getting Started

First you'll need to include the appropriate header files for sockets.

<u>Windows</u>

```c++	
# include <winsock.h>
```

Pass this to GCC: /lib/libws2_32.a
winsock as in Windows Socket

<u>Linux</u>

```cpp
# include <sys/type.h>
# include <sys/socket.h>
# include <netinet/in.h>
# include <arpa/inet.h>
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
	perror("Socket Creation FAILED!\n"); 
	return -1;
}
```

<u>Closing your first socket</u>

The difference here come from the way both OS's handle networking.

<u>Windows</u>

```cpp
closesocket(mySocket);
WSACleanup();
```

<u>Linux</u>

```cpp
close(mySocket);
```
#### Hosting a connection with your socket

There are three stages to host and establish a connection:

1. Bind the socket. Going back to this wall covered in wall plugs, this is where you take your socket and stick it into a plug.
2. Listen on the socket. This is where you sit and wait for someone on the outside world to try to connect to your socket.
3. Accept a connection. This is where you welcome them in and start talking.

<u>Binding to a socket</u>

Before you can bind to a socket you want to know what port you want to listen on. In this example I'll be listening on port "54377" because __I WANT__!

The `htons(int)` function basically converts a port number to the type that sockets prefer.

```cpp
address.sin_port = htons(54377);
address.sin_addr.s_addr = INADDR_ANY;
if(bind(mySocket, (struct sockaddr*)&address, sizeof(address))<0)
{
	perror("Binding Socket FAILED!\n");
	if(mySocket) close(mySocket);
	return -1;
}
```

<u>Listening on socket</u>

This function will **BLOCK** until someone tries to connect, so if your program hangs on this line and you're wondering why, it's because nobodies connected yet. The 5 refers to how many people can be trying to connect at once, not entirely sure about it tbh.

```cpp
printf("Listening on %d ... \n", 54377);
if(listen(mySocket, 5) < 0)
{
	printf("Listening on Socket Failed!\n");
	if(mySocket) close(mySocket);
	return -1;
}
```

<u>Accepting a conncetion</u>

The last stage. You'll need an object to get information about who you are connecting to, whose information you can read out of the struct to find out more about them after the function returns.

```cpp
struct sockaddr_in clientAddress;
if((mySocket = accept(mySocket, (struct sockaddr*)&clientAddress, sizeof(clientAddress))) < 0) 
{
	printf("Socket Connection FAILED!\n");
	if(mySocket) close(mySocket);
	return -1;
}
printf("Connection Established\n");
```

#### Connecting to a host

Thanksfully connecting to  a host is blissfully simple. This will be connecting to port 54377, the same port that we should be listening on above and it'll conncet to the local host(aka you), so you can try this stuff out.

```cpp
address.sin_port = htons(54377);
address.sin_addr.s_addr = inet_addr("127.0.0.1");
if(connect(mySocket, (struct sockaddr*)&address, sizeof(address)) < 0)
{
	printf("Socket Connection Failed!\n");
	if(mySocket) close(mySocket);
	return -1;
}
printf("Connected!\n");
```

#### Sending data over a socket

So you've got a socket set up at last, how do you send data over it?

The `send()` function takes the following:

1. The socket you want to send data over.
2. A char array containing your data you want to send.
3. An int containing the amount of data in the buffer.
4. An offset in the buffer incase you only want to send a part of it. __0__ means start from the beginning.

```cpp
send(mySocket, buffer, BUFFERSIZE, 0);
```
#### Receiving data from a socket

The `revc()` function takes the following:

1. The socket you want to receive data from.
2. A char array you want to store the data in.
3. The maximum size of the above array.
4. An offset in the buffer incase. __0__ starts from beginning.

The function returns the number of bytes that were received, up to the maximum you specified.

_WARNING_ - this function **BLOCK** until data arrives.

```cpp
int newData;
newData = recv(mySocket, buffer, BUFFERSIZE, 0);
```

#### My ways for writing both Windows and Unix

At the top of every file I start with two lines:

```cpp
#define __WINDOWS
#define __LINUX
```

and comment out which ever one I'm not using at the time.

This lets me do things like this:

```cpp
#ifdef __WINDOWS
#include <winsock.h>
#endif
#ifdef __LINUX
#include <sys/type.h>
#include <sys/socket.h>
#include <netinet/in.h>
#include <arpa/inet.h>
void closesocket(int socket) {close(socket);}
#endif
```

and

```cpp
#ifdef __WINDOWS
	WSADATA wsaData;
#endif
```

and

```cpp
#ifdef __WINDOWS
	WSAStartup(0x0202, &wsaData);
#endif
```

and 

```cpp
#ifdef __WINDOWS
	WSACleanup();
#endif
```

Notice how Linux makes it way easier to do networking.