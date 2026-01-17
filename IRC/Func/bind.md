In the context of setting up an IRC server (or any network server), **`bind`** is about telling the operating system **which IP address and port your server should listen on**.
Until a program binds to an address+port, it can’t receive incoming connections.
And bind attaches a socket to a IP adress and a port.
```c++
#include <sys/types.h>
#include <sys/socket.h>

int bind(int sockfd, struct sockaddr *my_addr, int addrlen);
```
- Sockfd in the socket fd got by [[socket]].
- Sockaddr is a pointer to a struct sockaddr that contains that contains info about the adress. See [[addrinfo]]
- addrlen is the length of bytes of that adress.
```c++
bind(sockfd, res->ai_addr, res->ai_addrlen);
```
