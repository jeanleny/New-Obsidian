Event 	Description
EPOLLIN 	File descriptor is available for read.

EPOLLOUT 	File descriptor is available for write.

EPOLLRDHUP 	Stream socket peer closed connection.

EPOLLPRI 	Exceptional condition on file descriptor.

EPOLLERR 	Error condition on file descriptor.

EPOLLHUP 	Hang up on file descriptor.

EPOLLET 	Set edge-triggered behavior for file descriptor.

EPOLLONESHOT 	Set one shot behavior for file descriptor.
(File descriptor is disabled after one event.)

EPOLLWAKEUP 	Ensure that system does not enter “suspend” or “hibernate” when this event is pending or is being processed. (EPOLLONESHOT and 

EPOLLET must be clear and the process should have the CAP_BLOCK_SUSPEND capability.)

EPOLLEXCLUSIVE 	Sets up the exclusive mode of wake up for the epoll file descriptor to which this file descriptor is being attached. Useful for avoiding the thundering herd problem in certain scenarios. 