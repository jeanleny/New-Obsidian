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

Stream Socket is using [[TCP-IP]] protocol.

Stream Socket are reliable two-way connected communication streams.
Its going to make the connection like a stream, you can either pull or send data through this stream.
Its just allow the full continuous stream of data without seing the chunking by setting packet of the datas, a continuous stream.
The stream socket is also called "reliable", wich means that even if the packets are sent not in right order, it will still be replaced/resent in the back by the TCP protocol.

But correcting data stream order or missing small data parts can have a cost depends on what we want to do, and the stream socket is, sometimes, not the right choice.
For exemple, if the data that are sents by the stream socket is being resent because a data is missing in the transmission, the video will get lag and will block to resend everything.
But this tiny missing data is just a frame that is barely visible by the user, so this socket is not the right one. 

With Datagram socket, we're using only **one data packet**, so no reliability, no resending/reordering.
The network will do the best effort to get the data, but if they get lost, they're lost.
We also never get **congestion control**, wich means data buffer overflow control. 
So we dont have any data restricion, but we could clog the network by sending to much data.
So its up to the project to use the right socket type.