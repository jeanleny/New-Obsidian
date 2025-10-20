It stand for Transmission Control Protocol / Internet Protocol.
It's the fundamental communication Protocol suite that the entire internet and most private networks run on.

it stands in a list of rules/standards wich are divided into layers

- The application layer is where the software operate (web browser, email client...)
- The transport layer is responsible for end to end communication. (like ports wich are numerical identifiers between services/application...)
- The internet layer manages the adressing and routing
- The physical layer wich is the physical transmission of data (cables).

Every device on network has his specific and unique IP.
It helps identify and locate devices on [[Lan]] and allows them to communicate with each other.
 We're using most of the time the IPv4 model.
 The IPv6 model has been added to solve the limitation problem of IPv4 due to bit registration.

A IPv4 is made of 32 bits splitted into 4 octets of bit each.
An octet can go from 0 to 255.

An IP adress has two parts :
The first 2 octets are the network and the 2 last are the host.
There is always two IP addresses reserved in a network.
1. The Network address (wich is the first IP of the network)
2. The Broadcast address (wich is the last IP of the network)

| Network     | Broadcast     |
| ----------- | ------------- |
| 192.168.1.0 | 192.168.1.255 |
255 is the number of bits in an octet.
So the usable IP range of these two addresses are :
192.168.1.1 <-> 192.168.1.254
This range represent a subnet.

# Subnet
- The subnet is sub network of a larger network.
- It defines a range of IP addresses of a network.
- It shows how many bits are used for the network and how many IP you can use.

| Network Address   | 192.168.42.0     |
| ----------------- | ---------------- |
| Broadcast Address | 192.168.42.127   |
| Subnet            | 192.168.42.0 /25 |
| Subnet Mask       | 255.255.255.128  |
The usable IP range is 192.168.42.1 - 192.168.42.126

The mask define how many bits belong to the network and many to the host.

| Subnet Mask     | CIDR notation | Network Bits | Host Bits | Total Hosts |
| --------------- | ------------- | ------------ | --------- | ----------- |
| 255.0.0.0       | /8            | 8            | 24        | 16.777.2141 |
| 255.255.0.0     | /16           | 16           | 16        | 65.534      |
| 255.255.255.0   | /24           | 24           | 8         | 254         |
| 255.255.255.192 | /26           | 26           | 6         | 62          |

Formula for usable hosts :
Usable Hosts = 2^h−2
h = number of **host bits** (bits not used for the network portion)
2^h = total possible addresses    
Subtract **2** because:
1 address is reserved for the **network address**
1 address is reserved for the **broadcast address**

So on a 255.255.0.0 Mask :
16 bits for the network : 32 bits of the total adress - 16 bits for network = 16 bits for host
2^16  - 2 = 65536 - 2 = 65534 usable hosts.

When we need to connect devices on differents subnets we need to use route to rely them

- **Host**: A computer that needs an IP and a gateway
    
- **Switch**: Connects hosts within the same subnet
    
- **Router**: Connects different subnets (and adds routing)

