Accept is the final step of receiving data on a port.
Each [[connect]] on port we are [[listen]] will queued up.
They will wait to be accepted with this function.
When you call it you get it to the pending connection wich will retrun you a **new socket** that we can use for this connection.
The original socket is still listening for more connection but the new one is used to get calls like [[send]] or [[recv]].
```c++
#include <sys/types.h>
#include <sys/socket.h>

int accept(int sockfd, struct sockaddr *addr, socklen_t *addrlen); 
```
- sockfd is the listening fd.
- addr is a pointer to a local sockaddr storage of the emitter. You can cast the type as a ``` (struct socakddr *)&addr```
- addrelen is the emitter size address
