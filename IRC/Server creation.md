In order to create a server

getaddrinfo()
socket()
bind()     ← choose local port
listen()
accept()

This allows us to use a client like netcat to connect to the server.