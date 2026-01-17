With the info we've get with [[getaddrinfo]], we can use socket to create the fd we can use later on sytem calls.
```c++
#include <sys/types.h>
#include <sys/socket.h>
int socket(int domain, int type, int protocol);
```
Those parameters allow you to set what kind of socket you want.
We can use what we get in the [[getaddrinfo]] before.
```c++
socket(res->ai_family, res->ai_socktype, res->ai_protocol);
```

Returns -1 on error.
