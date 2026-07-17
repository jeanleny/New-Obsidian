Connect a socket to a remote IP and port but it does it to a remote machine, usualy used for [[Client managing]].
```c++
#include <sys/types.h>
#include <sys/socket.h>

int connect(int sockfd, struct sockaddr *serv_addr, int addrlen); 
```
Sock fd is the clients socket that we use to connect to the serv_addr.
