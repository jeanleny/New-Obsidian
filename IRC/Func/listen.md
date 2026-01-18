This function is used to wait for incoming connection and handle them in some way. Its the step before [[accept]].
```c++
int listen(int sockfd, int backlog); 
```
- Sockfd is still the socket file from socket system call.
- Backlog is the number of connection allowed on the incoming queue.
It changes the **state** of the sockfd.
Sockfd is now a **passive** socket marked by the kernel as a **listening socket**, this socket is now able to receive incoming connection requests.

The kernel is creating a queue.
Incoming connections are going to wait in this queue until you [[accept]] them and **backlog** is how many can queue up.
Most of the time, we can set it up to 10.
