Here's the revised table with the full forms added:

| Protocol | Port Number | Full Form                           |
|----------|-------------|-------------------------------------|
| DNS      | 53 (UDP/TCP)| Domain Name System                  |
| DHCP     | 67 (UDP, server) <br> 68 (UDP, client) | Dynamic Host Configuration Protocol |
| SSH      | 22 (TCP)    | Secure Shell                        |
| FTP      | 20 (TCP, data transfer) <br> 21 (TCP, control) | File Transfer Protocol              |
| Telnet   | 23 (TCP)    | Telecommunication Network            |
| SMTP     | 25 (TCP)    | Simple Mail Transfer Protocol       |
| TFTP     | 69 (UDP)    | Trivial File Transfer Protocol      |
| HTTP     | 80 (TCP)    | Hypertext Transfer Protocol         |
| HTTPS    | 443 (TCP)   | Hypertext Transfer Protocol Secure  |
| POP3     | 110 (TCP)   | Post Office Protocol version 3      |
| IMAP4    | 143 (TCP)   | Internet Message Access Protocol    |
| SNMP     | 161 (UDP) (SNMP) <br> 162 (UDP) (SNMP traps) | Simple Network Management Protocol |
| NTP      | 123 (UDP)   | Network Time Protocol               |

Thank you for pointing that out!

### DHCP (Dynamic Host Configuration Protocol)

- **Port Number:** DHCP typically uses UDP ports 67 (server) and 68 (client).

- **DORA:** DHCP involves a four-step process known as DORA: 
  - **Discover:** The client broadcasts a request for IP address allocation.
  - **Offer:** The server responds with an offer of an IP address.
  - **Request:** The client formally requests the offered IP address.
  - **Acknowledge:** The server acknowledges the request and assigns the IP address to the client.

- **APIPA (Automatic Private IP Addressing):** If a DHCP client fails to obtain an IP address, it may assign itself an address from the reserved range 169.254.0.1 to 169.254.255.254.

- **Lease Time:** DHCP leases IP addresses to clients for a specific duration called the lease time.

- **Renew Time:** When a lease approaches expiration, the client attempts to renew the lease by contacting the DHCP server.

- **Unicast and Multicast:** DHCP communication can occur via unicast (between a client and server) or multicast (broadcasting to multiple clients simultaneously).


### DNS (Domain Name System)

- **Port Number:** DNS typically uses UDP and TCP port 53.

- **Query Types:** DNS supports various query types including:
  - **A:** Returns the IPv4 address associated with a domain name.
  - **AAAA:** Returns the IPv6 address associated with a domain name.
  - **CNAME:** Returns the canonical name for an alias.
  - **MX:** Returns the mail exchange servers for a domain.
  - **NS:** Returns the authoritative name servers for a domain.
  - **PTR:** Performs reverse DNS lookup, mapping an IP address to a domain name.
  - **TXT:** Returns text records associated with a domain.
  - **SOA:** Returns the start of authority record for a zone.

- **Records:** DNS stores various types of records to map domain names to IP addresses and perform other functions. Some common records include:
  - **A Record:** Maps a domain name to an IPv4 address.
  - **AAAA Record:** Maps a domain name to an IPv6 address.
  - **CNAME Record:** Creates an alias for a domain name.
  - **MX Record:** Specifies the mail servers responsible for receiving email on behalf of a domain.
  - **NS Record:** Specifies the authoritative name servers for a domain.
  - **PTR Record:** Maps an IP address to a domain name for reverse DNS lookups.
  - **TXT Record:** Stores arbitrary text information associated with a domain.

- **Zones:** DNS divides the domain name space into zones, which are administrative units managed by specific name servers. Each zone consists of one or more domain names and their associated records. Zones can be authoritative (primary or secondary) or caching (resolver) zones.


### TCP (Transmission Control Protocol)

#### Functions and Features:
- **Reliable Data Transmission:** TCP ensures reliable delivery of data by using acknowledgments, sequence numbers, and retransmissions.
- **Flow Control:** TCP regulates the flow of data between sender and receiver to prevent congestion and ensure efficient transmission.
- **Connection-Oriented:** TCP establishes a connection before data transfer and ensures orderly termination of the connection afterward.
- **Error Detection and Correction:** TCP uses checksums to detect errors in transmitted data and can request retransmission of corrupted segments.
- **Full Duplex Communication:** TCP supports simultaneous data transfer in both directions.
- **Multiplexing:** TCP allows multiple applications on a host to use the network simultaneously.

#### TCP Header:
The TCP header contains several fields, including source and destination port numbers, sequence and acknowledgment numbers, TCP flags, window size, checksum, and urgent pointer.

#### TCP Flags:
TCP flags, also known as control bits, include:
- SYN: Synchronize sequence numbers for connection establishment.
- ACK: Acknowledge received data.
- FIN: Indicates the sender has finished sending data.
- RST: Reset the connection.
- URG: Indicates urgent data.
- PSH: Push function, which requests immediate data delivery without buffering.
- CWR and ECE: Congestion window reduced and ECN-Echo, related to congestion control.

#### TCP Timer:
TCP uses several timers, including retransmission timers (for retransmitting lost segments), persist timers (for retransmitting zero-window probes), and keep-alive timers (to check if the connection is still alive).

#### Window Size:
The window size indicates the amount of data that can be sent before receiving an acknowledgment. It helps regulate the flow of data and prevents congestion.

#### Checksum:
The TCP checksum is used for error detection. It covers the TCP header and data payload to ensure data integrity during transmission.

#### Urgent Pointer:
The urgent pointer is used to indicate the presence of urgent data in a segment.

#### Options and Padding:
TCP options include Maximum Segment Size (MSS), Window Scaling, Selective Acknowledgment (SACK), and Timestamps. Padding is used to ensure that the TCP header ends on a 32-bit boundary.

#### Three-Way Handshake:
1. Client sends a SYN packet to the server.
2. Server responds with SYN-ACK, acknowledging the client's SYN.
3. Client sends an ACK packet, acknowledging the server's SYN-ACK. At this point, the connection is established.

#### Four-Way Handshake:
1. Initiator sends FIN packet to initiate termination.
2. Responder sends ACK to acknowledge the FIN.
3. Responder sends its own FIN packet to initiate termination from its end.
4. Initiator sends ACK to acknowledge the FIN.

#### MTU (Maximum Transmission Unit):
MTU is the maximum size of a single packet that can be transmitted on a network. It is important in TCP/IP networking for efficient data transmission.

#### Congestion Control:
TCP uses various mechanisms to handle congestion, including:
- **Three Duplicate ACKs:** Indicates network congestion, prompting TCP to reduce its transmission rate.
- **Retransmission Timeout:** Occurs when a segment is not acknowledged within a certain time, indicating congestion, leading to retransmission.
- **Congestion Avoidance:** TCP reduces its transmission rate upon congestion detection, gradually increasing it to find the optimal rate.

#### Action Taken upon Congestion:
- **Mild Action:** Reduce the transmission rate by a small factor.
- **Strong Action:** Drastically reduce the transmission rate or temporarily halt data transmission to alleviate congestion.


### SMTP (Simple Mail Transfer Protocol)
- **Port Number:** SMTP typically uses TCP port 25.
- **Working:** SMTP is a protocol used for sending email messages between servers. When you send an email, your email client communicates with your email server using SMTP. The email server then relays the message to the recipient's email server, which is also done via SMTP. Finally, the recipient's email server stores the message until the recipient retrieves it.

### POP3 (Post Office Protocol version 3)
- **Port Number:** POP3 typically uses TCP port 110.
- **Working:** POP3 is a protocol used for retrieving email messages from an email server to a client device. When you check your email using a POP3 client (like Outlook or Thunderbird), the client connects to the email server and downloads any new messages to your device. By default, POP3 downloads the messages to your device and typically deletes them from the server, although there are options to keep copies on the server.

### IMAP (Internet Message Access Protocol)
- **Port Number:** IMAP typically uses TCP port 143.
- **Working:** IMAP is also used for retrieving email messages from an email server to a client device, similar to POP3. However, IMAP offers more advanced features compared to POP3. With IMAP, emails are stored on the server rather than being downloaded to the client device. This allows for easier access to emails from multiple devices since the emails remain synchronized across devices. IMAP also supports organizing emails into folders on the server, allowing for better management of email messages.


### SSL (Secure Sockets Layer) and TLS (Transport Layer Security)

#### Working:
- **SSL and TLS** are cryptographic protocols designed to provide secure communication over a computer network.
- They establish an encrypted connection between a client (such as a web browser) and a server (such as a website).
- SSL was the predecessor of TLS, and TLS is the more modern and secure version.
- These protocols ensure confidentiality, integrity, and authenticity of data transmitted over the network.

#### SSL Handshake (TLS Handshake):
- **ClientHello:** The client sends a message containing supported SSL/TLS versions, supported cipher suites, and other parameters.
- **ServerHello:** The server responds with the chosen SSL/TLS version, selected cipher suite, and other parameters.
- **Key Exchange:** The server sends its public key or certificate to the client, and the client verifies the certificate.
- **Client Authentication (Optional):** If required, the client may authenticate itself to the server using a certificate.
- **Pre-master Secret:** The client generates a random pre-master secret, encrypts it with the server's public key, and sends it to the server.
- **Session Keys Generation:** Both client and server use the pre-master secret to independently generate session keys for encrypting and decrypting data.
- **Finished Messages:** Both parties exchange "finished" messages to confirm that the handshake is complete and that subsequent communication will be encrypted.

#### Symmetric Encryption:
- **Symmetric encryption** uses the same key for both encryption and decryption.
- It's fast and efficient for encrypting large amounts of data.
- Common symmetric encryption algorithms include AES (Advanced Encryption Standard) and DES (Data Encryption Standard).

#### Asymmetric Encryption and Formation of Key:
- **Asymmetric encryption** uses a pair of keys: a public key for encryption and a private key for decryption.
- The public key can be freely distributed, while the private key is kept secret.
- To form a key using asymmetric encryption, one party (e.g., the client) generates a public-private key pair and shares the public key with the other party (e.g., the server).
- The other party uses the received public key to encrypt a message and sends it back.
- The original party decrypts the message using its private key.

#### Hash Function:
- **Hash functions** are cryptographic algorithms that generate a fixed-size hash value from input data of any size.
- They are used for data integrity verification and digital signatures.
- Hash functions should produce a unique hash value for each unique input.
- Common hash functions include SHA-256 (Secure Hash Algorithm 256-bit) and MD5 (Message Digest Algorithm 5).


### Hub:
- **Functionality:** A hub is a basic networking device that operates at the physical layer (Layer 1) of the OSI model.
- **Operation:** It receives data from one device and broadcasts it to all other devices connected to the hub.
- **Collision Domain:** All devices connected to a hub share the same collision domain, leading to collisions and reduced network efficiency.
- **Not Common:** Hubs are not commonly used in modern networks due to their limitations in performance and collision handling.

### Router:
- **Functionality:** A router is a networking device that operates at the network layer (Layer 3) of the OSI model.
- **Operation:** It forwards data packets between different networks based on IP addresses.
- **Routing Table:** Maintains a routing table to determine the best path for data transmission.
- **NAT:** Can perform Network Address Translation (NAT) to allow multiple devices on a local network to share a single public IP address.
- **Firewall:** Often includes firewall capabilities for network security.

### Switch:
- **Functionality:** A switch is a networking device that operates at the data link layer (Layer 2) of the OSI model.
- **Operation:** It forwards data packets between devices within the same network based on MAC addresses.
- **MAC Table:** Maintains a MAC address table to determine the port to which a packet should be forwarded.
- **Collision Domain:** Each port on a switch has its collision domain, leading to improved network performance compared to hubs.
- **VLAN:** Supports Virtual LAN (VLAN) segmentation for network organization and security.

### Bridge:
- **Functionality:** A bridge is a networking device that operates at the data link layer (Layer 2) of the OSI model.
- **Operation:** It connects multiple network segments and forwards data between them based on MAC addresses.
- **Similarity to Switch:** Bridges are similar to switches in functionality, but they typically have fewer ports and are used to connect smaller network segments.
- **MAC Table:** Like switches, bridges maintain a MAC address table for packet forwarding.

### Key Differences:
- **Layer of Operation:** Hubs operate at Layer 1, switches and bridges at Layer 2, and routers at Layer 3.
- **Forwarding Mechanism:** Hubs broadcast data to all connected devices, switches and bridges forward data based on MAC addresses within the same network, while routers forward data based on IP addresses between different networks.
- **Collision Handling:** Hubs have a single collision domain, switches and bridges have per-port collision domains, and routers do not have collision domains as they operate at Layer 3.


### ARP (Address Resolution Protocol):
- **Functionality:** ARP is used to map IP addresses to MAC addresses within a local network.
- **Operation:** When a device needs to communicate with another device on the same network, it uses ARP to discover the MAC address corresponding to the IP address.
- **Request-Reply Mechanism:** A device sends an ARP request broadcast containing the IP address it wants to reach, and the device with that IP address replies with its MAC address.
- **ARP Cache:** Devices maintain an ARP cache to store recently resolved IP-to-MAC mappings for faster future communication.

### Types of ARP:
1. **ARP:** Standard Address Resolution Protocol used to resolve IPv4 addresses to MAC addresses.
2. **RARP (Reverse ARP):** Used to resolve MAC addresses to IP addresses, primarily in diskless workstation environments. Less common nowadays due to DHCP.
3. **Proxy ARP:** A technique where a device responds to ARP requests on behalf of another device, typically used in network address translation (NAT) scenarios.
4. **Gratuitous ARP (GARP):** An unsolicited ARP message where a device announces its own IP-to-MAC mapping to update the ARP caches of other devices.

### Gratuitous ARP (GARP):
- **Functionality:** GARP is used to update the ARP caches of other devices on the network with a new MAC address mapping for an IP address.
- **Usage:** It can be used for network redundancy, IP address conflicts resolution, or updating ARP caches after network reconfiguration.
- **Difference from ARP:** Unlike ARP, which is initiated when a device needs to resolve an IP address, GARP is sent proactively by a device to inform other devices of its own IP-to-MAC mapping changes.

### Inverse ARP (InARP):
- **Functionality:** Inverse ARP is used in Frame Relay and ATM networks to resolve network layer addresses (IP addresses) from data link layer addresses (DLCIs in Frame Relay or VPI/VCI in ATM).
- **Operation:** InARP messages are sent between the router and the switch or access device to map DLCIs or VPI/VCI to IP addresses.
- **Purpose:** It allows routers in Frame Relay or ATM networks to dynamically learn the mapping between network layer addresses and data link layer addresses without manual configuration.

### IP Addressing (IPv4)
- **Classification:** IPv4 addresses are classified into five classes: A, B, C, D, and E. Each class has a range of addresses determined by the first few bits of the address.
- **Broadcast Domain:** A broadcast domain is a network segment within which broadcast messages can reach all devices. In IPv4, devices in the same subnet (determined by the subnet mask) belong to the same broadcast domain.
- **Finding Broadcast Domain:** To find the broadcast domain in IPv4, determine the network address using bitwise AND operation between the IP address and subnet mask. Then, the broadcast address is the network address with all host bits set to 1. All devices with IP addresses within this range are in the same broadcast domain.

### How to find network ID's
To find the network ID of an IPv4 address, you perform a bitwise AND operation between the IP address and its subnet mask. This operation preserves the network portion of the address and sets the host portion to 0, giving you the network ID.

### NAT (Network Address Translation):
- **Usage:** NAT is used to translate private IP addresses of devices within a local network into a single public IP address for communication over the internet.
- **Purpose:** It allows multiple devices within a local network to share a single public IP address, conserving IPv4 address space and providing an additional layer of security by hiding internal IP addresses from external networks.
- **Operation:** NAT works by modifying the source and/or destination IP addresses in IP packets as they traverse a NAT-enabled router or firewall.
- **Types:** 
  - **Static NAT:** Maps a private IP address to a specific public IP address, typically used for hosting servers.
  - **Dynamic NAT:** Maps private IP addresses to public IP addresses from a pool of available addresses dynamically.
  - **PAT (Port Address Translation):** A form of dynamic NAT where multiple private IP addresses are mapped to a single public IP address using different port numbers.

### PAT (Port Address Translation):
- **Usage:** PAT, also known as NAT overload, is a variation of NAT commonly used in home and small office networks.
- **Purpose:** It allows multiple devices within a local network to share a single public IP address by using different port numbers to distinguish between connections.
- **Operation:** PAT maps each private IP address and port number combination to a unique public IP address and port number, enabling multiple devices to establish simultaneous connections over the internet.
- **Benefits:** PAT conserves public IP addresses, enhances security by masking internal IP addresses, and facilitates communication for devices within the local network.

## VLSM
VLSM, or Variable Length Subnet Masking, allows for the allocation of IP addresses more efficiently by permitting different subnets to have varying subnet mask lengths. This flexibility enables the creation of subnets tailored to specific requirements, optimizing IP address utilization. 

## ACL
ACLs, or Access Control Lists, are used to control network traffic by defining rules that either permit or deny packets based on specified criteria. These criteria typically include factors like source/destination IP addresses, protocols, port numbers, and interface directions. ACLs enhance network security and performance by regulating traffic flow at network devices such as routers, switches, and firewalls.

## SUPERNETTING
Supernetting, also known as route aggregation, involves combining multiple contiguous subnets into a single larger subnet. This process reduces the size of routing tables by summarizing several subnets as a single entry. By aggregating subnets, supernetting conserves memory and processing resources in routers, decreases routing table size, and improves routing scalability.


### Fragmentation and Segmentation

**Fragmentation:**
- **Definition:** Fragmentation occurs when a large data packet is broken into smaller fragments to fit within the Maximum Transmission Unit (MTU) size of the network.
- **Usage:** Fragmentation is typically performed by routers when forwarding packets between networks with different MTU sizes.
- **Result:** Each fragment retains a portion of the original packet's data and a fragment header to indicate its position within the original packet.
- **Purpose:** Fragmentation ensures that data can be transmitted across networks with varying MTU sizes while adhering to size constraints.

**Segmentation:**
- **Definition:** Segmentation involves dividing a large data stream into smaller segments at the transport layer of the OSI model.
- **Usage:** Segmentation is performed by transport layer protocols such as TCP to optimize data transmission and manage flow control.
- **Result:** Each segment contains a portion of the original data along with transport layer headers for routing and sequencing.
- **Purpose:** Segmentation improves network performance by efficiently transmitting data in smaller, manageable units and allows for reliable data delivery through features like sequence numbering and acknowledgment.

**Difference:**
- **Fragmentation** occurs at the network layer (Layer 3) and is primarily performed by routers to accommodate differing MTU sizes between networks, whereas **segmentation** occurs at the transport layer (Layer 4) and is performed by transport layer protocols to optimize data transmission and manage flow control.
- Fragmentation breaks large packets into smaller fragments for transmission across networks, while segmentation divides data streams into smaller segments for efficient transport and reliable delivery within a network.

### HTTP (Hypertext Transfer Protocol)
- **Port Number:** HTTP typically uses TCP port 80.
- **Usage:** HTTP is a protocol used for transmitting hypertext documents, such as HTML files, over the internet.
- **Security:** HTTP does not provide encryption for data transmission, making it vulnerable to interception and manipulation by malicious actors.
- **Example:** `http://www.example.com` 

### HTTPS (HTTP Secure)
- **Port Number:** HTTPS typically uses TCP port 443.
- **Usage:** HTTPS is a secure version of HTTP that uses encryption to ensure secure communication between a client and a server.
- **Security:** HTTPS encrypts data transmitted between the client and server, preventing eavesdropping and tampering.
- **Example:** `https://www.example.com`

**Difference:**
- The main difference between HTTP and HTTPS is the security aspect. HTTP transmits data in plaintext, while HTTPS encrypts data using SSL/TLS protocols, providing secure communication over the internet.
- HTTPS is preferred for transmitting sensitive information such as passwords, credit card numbers, and personal data, as it ensures confidentiality and integrity of data during transmission.


### OSPF (Open Shortest Path First)
 OSPF is a dynamic routing protocol used to determine the shortest path to destinations within an IP network. It employs various mechanisms such as AD values, DR/BDR election, packet types, and LSAs to maintain network connectivity and provide efficient routing.

#### Administrative Distance (AD) Value:
- **Definition:** OSPF assigns a default administrative distance (AD) value of 110 to its routes.
- **Usage:** AD is used by routers to determine the preferred route when multiple routing protocols are present.
- **Example:** If OSPF and another routing protocol advertise routes to the same destination, the router will prefer the OSPF route due to its lower AD value.

#### DR (Designated Router) and BDR (Backup Designated Router) Election:
- **Purpose:** In multi-access network segments (e.g., Ethernet), OSPF elects a DR and BDR to reduce OSPF overhead and optimize network efficiency.
- **Operation:** OSPF routers on the segment elect a DR and BDR based on their Router ID (RID). The DR and BDR are responsible for sending and receiving OSPF updates on behalf of the network segment.
- **Example:** In a LAN segment with multiple OSPF routers, the router with the highest priority or highest RID becomes the DR, and the router with the second-highest priority becomes the BDR.

#### OSPF Broadcast Network Types:
- **Definition:** OSPF supports several network types, including broadcast, point-to-point, point-to-multipoint, and non-broadcast multi-access (NBMA).
- **Usage:** The broadcast network type is commonly used for Ethernet LANs where OSPF routers can communicate with each other through broadcast messages.
- **Example:** OSPF routers on an Ethernet LAN use OSPF hello packets to discover neighbors and elect a DR and BDR.

#### OSPF IP Addresses:
- **Usage:** OSPF uses IP addresses for router identification (RID) and neighbor identification.
- **Example:** Each OSPF router is assigned a unique RID, typically the highest IP address on a loopback interface, to identify itself within the OSPF domain.

#### OSPF Packet Types:
- **Hello Packets:** Used for neighbor discovery, adjacency formation, and DR/BDR election.
- **Database Description (DBD) Packets:** Used to exchange information about the OSPF link-state database during adjacency formation.
- **Link State Request (LSR) Packets:** Used to request specific link-state advertisements (LSAs) from OSPF neighbors.
- **Link State Update (LSU) Packets:** Used to advertise new or updated LSAs to OSPF neighbors.
- **Link State Acknowledgment (LSAck) Packets:** Used to acknowledge received LSAs.

#### OSPF Packet with LSA (Link State Advertisement) and Types:
- **LSA Definition:** LSAs contain information about the state of OSPF routers and links within an OSPF area.
- **LSA Types:**
  - **Router LSA (Type 1):** Advertises router information, including the router's own link-state and the state of its interfaces.
  - **Network LSA (Type 2):** Advertises information about multi-access networks, including the DR and connected routers.
  - **Summary LSA (Type 3, 4, and 5):** Advertises routes from one area to another.
  - **AS External LSA (Type 5):** Advertises routes external to the OSPF domain.
  - **Link Local LSA (Type 9):** Advertises IPv6 link-local addresses.
  - **Intra-Area-Prefix LSA (Type 9):** Advertises IPv6 prefixes within an OSPF area.

Certainly!

### EIGRP (Enhanced Interior Gateway Routing Protocol)
EIGRP is known for its efficient use of bandwidth, fast convergence, and support for multiple network technologies. By using advanced algorithms and packet types, EIGRP ensures reliable and scalable routing in complex network environments.

#### Administrative Distance (AD) Value:
- **Definition:** EIGRP assigns a default administrative distance (AD) value of 90 to its routes.
- **Usage:** AD is used by routers to determine the preferred route when multiple routing protocols are present.
- **Example:** If EIGRP and another routing protocol advertise routes to the same destination, the router will prefer the EIGRP route due to its lower AD value.

#### Working:
- **Operation:** EIGRP is an advanced distance-vector routing protocol that uses a combination of Diffusing Update Algorithm (DUAL) and distance-vector algorithms.
- **Features:** EIGRP maintains a topology table, routing table, and neighbor table to exchange routing information and calculate the best routes.
- **DUAL Algorithm:** Ensures loop-free and fast convergence by providing loop prevention and route calculation mechanisms.
- **Convergence:** EIGRP supports fast convergence by sending partial updates and using feasible successors for backup routes.

#### EIGRP Packet Types:
- **Hello Packets:** Used for neighbor discovery and to maintain neighbor relationships.
- **Update Packets:** Used to exchange routing information, including reachable destinations and associated metrics.
- **Query Packets:** Sent by a router when it loses a route and queries neighboring routers for an alternative path.
- **Reply Packets:** Sent in response to query packets to provide information about alternative routes.
