Epoll is a function that can manage multiple connection ([[Multiplexing]]) by organising fd's.
There's a few function to set all that up, in order :

Epoll is an instance of fd's management so we need to create it with **epoll_create1()**.

```c++
int epoll_create1(int flags);
```
epoll_create takes a flags wich can be 0 for nothing or EPOLL_CLOEXEC to close on exec.
Return a an epoll instance fd.
# epoll_event
Epoll will manage these fd's by using an event structure called **epoll_event**.
```c++
struct epoll_event {
    uint32_t events;   // WHAT happened / what you want
    epoll_data_t data; // WHO it happened to
};
```
The events is a bitmask where we put flags.
In our case we will set it on **EPOLLIN** which is the flag to read without blocking anything. **EPOLLOUT** is to write without blocking.
So the **fd listener** will wait for incoming connection, and the **client socket fd** will wait for incoming IRC data.

Data is another union structure that store few things.
```c++
typedef union epoll_data {
    void     *ptr;
    int       fd;
    uint32_t  u32;
    uint64_t  u64;
} epoll_data_t;
```
Ptr is used to identify the address of the incoming/emitter connection.
For our server we will fill the fd field with the **listener fd**.
```c++
struct epoll_events event;

event.events = EPOLLIN
event.data.fd = listener
```

# epoll_ctl

Now we want to register FD's in our epoll instance.
```c++
int epoll_ctl(int epfd, int op, int fd,
                     struct epoll_event *_Nullable event);
```

With this function we explicitly tell epoll what to watch.
- epfd id the epoll instance fd
- op is the flag to set what operation we want epoll_ctl to do. [[epoll_ctl op]]
- fd for wich we want to do the control operation.
- event is the structure seen before (**epoll_events**).

In our case we will set op with EPOLL_CTL_ADD wich will add the fd to the set of file descriptor monitored by the epoll instance (epfd).
The events to be monitored are given in the epoll_event structure.

# epoll_wait

Next we want our server to wait for an event.
Epoll_wait waits until at least one event has occurred on the epoll instance or the timeout is reached.
Once epoll_wait has stopped, it returns the **number of fd ready for I/O** and all the events are stored in a **epoll_event structure**.
So these events tells you :
Wich fd
What kind of event happened.
```c++
int epoll_wait (int epfd, struct epoll_event *events, 
                int maxevents, int timeout);
```
- Epfd is the epoll instance fd
- events is the structure that will store the events
- max event is the event's limit.
- timeout is in milisecond.

Now epoll told us which FD's we can work with, we have to set our routine to get what these files are sending us.