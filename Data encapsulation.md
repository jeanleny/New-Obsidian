![[Pasted image 20260116150500.png]]

Data encapsulation is just the path that do the data from the creation of the packet through all the protocol he goes by until the physical layer (ethernet).

Exemple :

1. **Application layer** :
Contains the data "Hello world"

2. **Transport Layer** (Protocol here is TCP)
Add a 
- source port
- destination port
- The sequence numbers (TCP)
Now it knows _which application_ should receive the data.

3. Network Layer (IP)
Adds an IP :
- Source IP adress
- Destination IP adress
Now it knows _which machine_ should receive the data.

4. Data link layer (ethernet/wifi)
Adds :
- Frame header(MAC addresses)
- Frame trailer (error checking)
Now it knows _how to deliver the data on the local network_.

5. Physical Layer
The whole thing becomes an electronic signal/radio waves ...