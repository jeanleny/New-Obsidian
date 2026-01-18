Epoll is a function that can manage multiple connection ([[Multiplexing]]) by organising fd's.
There's a few function to set all that up, in order :

Epoll is an instance of fd's management so we need to create it with **epoll_create()**.

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
Ptr is used to identify the adress of the incoming/emitter connection.
For our server we will fill the fd field with the **listener fd**.
```c++
struct epoll_events event;

event.events = EPOLLIN
event.data.fd = listener
```
