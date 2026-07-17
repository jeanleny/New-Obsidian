getaddrinfo take 3 input parameters and 1 pointers to a linked list called res.

```c++
#include <sys/types.h>
#include <sys/socket.h>
#include <netdb.h>

int getaddrinfo(const char *node,   // e.g. "www.example.com" or IP
                const char *service,  // e.g. "http" or port number
                const struct addrinfo *hints,
                struct addrinfo **res);
```
- **Node** is the host name to connect to (like www.google.com) or an IP adress
- **Service** can be a port number (like 4242) or the name of a particular service [iana](https://www.iana.org/assignments/service-names-port-numbers/service-names-port-numbers.xhtml)
-  **Hints** points to a struct [[addrinfo]] where we filled our information.