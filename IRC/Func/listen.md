This function is used to wait for incoming connection and handle them in some way. Its the step before [[accept]].
```c++
int listen(int sockfd, int backlog); 
```
- Sockfd is still the socket file from socket system call.
- Backlog is the number of connection allowed on the incoming queue.
Incoming connections are going to wait in this queu until you [[accept]] them and this is the limit on how many can queue up.
Most of the time, we can set it up to 10.
