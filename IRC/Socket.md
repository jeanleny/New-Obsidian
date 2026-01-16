Sockets are : a way to speak to other programs using standard Unix [[File descriptor]].

To get this socket file descriptor, you can use [socket()](https://man7.org/linux/man-pages/man2/socket.2.html)
You can communicate with it by using [recv()](https://man7.org/linux/man-pages/man2/recv.2.html) and [send()](https://man7.org/linux/man-pages/man2/send.2.html) wich are socket calls.

There are several type of sockets, DARPA internet adresses(internet sockets),
path names on a local node (UNIX socket)...

all of these sockets are listed on [sys/socket.h](https://pubs.opengroup.org/onlinepubs/7908799/xns/syssocket.h.html)

We will focus on INTERNET sockets, specially 2 types of internet sockets.

# Stream Socket and Datagram Socket

Defines :
Stream socket ref : SOCK_STREAM
Datagram socket ref : SOCK_DGRAM

Internet Socket are using TCP protocol

Stream Socket are reliable two-way connected communication streams.


Datagram socket are sometimes called "connectionless sockets"


