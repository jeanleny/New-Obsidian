Secure Sockets Layer
Transport Layer Security
Theses are protocols that uses both message authentication codes.
Its a cryptographic technique that checks message intergrity and authenticity.

We often talk about symmetric encryption.
Its means that **each sides uses the same encryption/decryption key to transfer data**


How does it works :
- The clients contacts the server using a secure URL.(HTTPS)
- The server sends the client its certificate and public key
- The server verifies it.
- The client and the server negotiate the strongest type of encryption that each can support.
- THe client encypts a secret session key with the server's public key and sends it back to the server.
- The server decrypts the client communication with its private key, and the session is estavblished.
- The session key (symetric encryption) is now used to encrypt and decrypt data transmitted between the client and server.