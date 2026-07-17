```c++
struct addrinfo {
    int              ai_flags;     // AI_PASSIVE, AI_CANONNAME, etc.
    int              ai_family;    // AF_INET, AF_INET6, AF_UNSPEC
    int              ai_socktype;  // SOCK_STREAM, SOCK_DGRAM
    int              ai_protocol;  // use 0 for "any"
    size_t           ai_addrlen;   // size of ai_addr in bytes
    struct sockaddr *ai_addr;      // struct sockaddr_in or _in6
    char            *ai_canonname; // full canonical hostname
    struct addrinfo *ai_next;      // linked list, next node
};
```
This struct contains the parameters of a socket we want to setup.

- **ai_flags** is for additional options see [man](https://man7.org/linux/man-pages/man3/getaddrinfo.3.html), AI_PASSIVE fills the ip for you
- **ai_family** specifies the adress type (IPV4 OR IPV6) you can set AF_UNSPEC for any
- **ai_socktype** specifies the preferred type like SOCK_STREAM or SOCK_DGRAM. 0 is for any type.
- **ai_protocol** is for the protocol transmission, TCP,DUP. 0 is for any.
- **ai_addr** is pointer to another structure wich contains address information of the socket Like so :
```c++
struct sockaddr {
    unsigned short    sa_family;    // address family, AF_xxx
    char              sa_data[14];  // 14 bytes of protocol address
}; 
```
the family is the type of adress (ipv4/6).