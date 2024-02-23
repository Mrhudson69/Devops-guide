## OSI Reference Model

Open Systems Interconnection (OSI) is a network architecture model standardized by the International Organization for Standardization (ISO). The OSI model defines a framework for understanding and implementing networking protocols.

### Key Points:

- **Seven Layers:** The OSI model consists of seven layers, each serving a specific purpose in the communication process.
- **Layer Abstraction:** Layers are added to the model to abstract different aspects of network communication, allowing for easier management and troubleshooting.
- **Well-Defined Functions:** Each layer has a distinct set of functions and responsibilities, ensuring clear separation of concerns and modular design.
- **Standardized Protocols:** The functions of each layer are defined by internationally standardized protocols, ensuring interoperability between different networking devices and systems.

### Principles:

1. **Abstraction:** Create a new layer whenever a different abstraction is required to address specific networking concerns.
2. **Well-Defined Functions:** Ensure that each layer has a clearly defined function that contributes to the overall communication process.
3. **Standardized Protocols:** Base the function of each layer on internationally recognized and standardized protocols to facilitate compatibility and interoperability.

# 7 Layers

1. **Physical layer**
2. **Data link layer**
3. **Network layer**
4. **Transport layer**
5. **Session layer**
6. **Presentation layer**
7. **Application layer**

# TCP and UDP

**Transmission Control Protocol (TCP):**
- Establishes a secure communication line to ensure reliable transmission.
- Verifies the receipt of messages to ensure all data was successfully transferred.
- Broadcasting is not supported.
- Commonly used for email, texting, file transfers, and web browsing.

# TCP Flags

TCP (Transmission Control Protocol) uses flags within its header to control various aspects of the communication between two endpoints. These flags provide information about the state of a TCP connection and help manage the flow of data. Here's an overview of the TCP flags:

1. **URG (Urgent)**:
   - Indicates that the data carried in the segment is urgent and should be prioritized by the receiving endpoint.

2. **ACK (Acknowledgment)**:
   - Indicates that the acknowledgment field is valid. This flag is used to acknowledge received data and confirm successful receipt.

3. **PSH (Push)**:
   - Instructs the receiving endpoint to deliver data to the application layer immediately without waiting to accumulate a full segment.

4. **RST (Reset)**:
   - Resets a TCP connection. This flag is used to indicate an abnormal termination of the connection and requests a reset of the connection on both ends.

5. **SYN (Synchronize)**:
   - Initiates a connection establishment between two endpoints. When a SYN flag is set in a segment, it indicates that the sender wants to synchronize sequence numbers to establish a new connection.

6. **FIN (Finish)**:
   - Indicates the sender's intention to terminate the connection. When a FIN flag is set, it means that the sender has finished sending data and wants to close the connection.


**User Datagram Protocol (UDP):**
- Sends data without confirming receipt or checking errors, which may result in some or all data being lost during transmission.
- Supports broadcasting.
- Ideal for live streaming, online gaming, and video chat.

# UDP Flags

UDP (User Datagram Protocol) is a connectionless protocol that does not use flags in the same way as TCP. Unlike TCP, UDP does not have a header field dedicated to flags. However, there are certain characteristics and behaviors of UDP that can be considered analogous to flags in TCP:

1. **Checksum**:
   - UDP includes a checksum field in its header, which is used to detect errors in the transmitted data. While not a flag in the traditional sense, the checksum serves a similar purpose by providing a mechanism for error detection.

2. **Length**:
   - UDP includes a length field in its header, which specifies the length of the UDP datagram, including the header and data. While not a flag, the length field provides information about the size of the datagram.

3. **Source Port and Destination Port**:
   - UDP uses source and destination port numbers in its header to identify the source and destination applications or services. While not flags, these port numbers serve as identifiers for the endpoints of the communication.

4. **No Congestion Control**:
   - Unlike TCP, UDP does not implement congestion control mechanisms such as flow control or congestion avoidance. While not represented as flags, this characteristic distinguishes UDP from TCP and influences its behavior in network communications.

5. **Connectionless and Unreliable**:
   - UDP is a connectionless and unreliable protocol, meaning it does not establish a connection before transmitting data and does not guarantee delivery of packets. While not flags, these characteristics affect the way UDP operates and are important considerations when designing network applications.

While UDP does not have flags in the same sense as TCP, understanding its header fields and characteristics is crucial for effectively using the protocol and designing network applications that rely on UDP for communication.


# Networking Devices

**Network**
- two or more devices connnected in a group to share data is called network.

**Gateway**
- A gateway is a network node that connects two networks using different communication protocols. It acts as a bridge between two networks and enables data and information to be exchanged between them

**firewall**
- A firewall is a security system that monitors and controls incoming and outgoing network traffic based on predetermined security rules. It is used to protect private networks from unauthorized access and to filter the traffic passing through a network

**VLAN**
- A VLAN (Virtual Local Area Network) is a logical grouping of network devices that behave as if they are on the same local network, even though they may be physically located on different networks

**Subnet**
- A subnet is a logical subdivision of an IP network. It is typically used to divide an IP network into two or smaller networks in order to improve network performance and security. Each subnet is identified by a unique subnet mask.

**broadcast domain**
- A broadcast domain is a logical division of a computer network in which all nodes can reach each other by broadcast at the data link layer. Moreover, a broadcast domain can be within the same LAN segment, or it can span multiple LAN segments.

**collision domain**
- A collision domain is a network segment in which data packets can collide with each other when they are sent on a shared network segment. In addition, it is generally caused by a network design problem, such as using hubs instead of switches or when multiple devices are connected to the same switch port.

**VPN**
- A Virtual Private Network (VPN) is a private network connection that is created by using the public Internet. Subsequently, it permits users to send and receive data securely and anonymously by routing their traffic through a secure tunnel

**Types of VPN**
1. **Access VPN:** 
   - Provides connectivity to remote mobile users and telecommuters.
   - Alternative to dial-up or ISDN connections.
   - Low-cost solution with wide connectivity.

2. **Site-to-Site VPN:** 
   - Connects networks of different office locations.
   - **Sub-categories:**
     - *Intranet VPN:* Connects remote offices using shared infrastructure with same accessibility policies as private WAN.
     - *Extranet VPN:* Connects suppliers, customers, partners, etc., over shared infrastructure using dedicated connections.

**IP address**
- An IP address (Internet Protocol address) is a numerical label assigned to each device connected to a computer network that uses the Internet Protocol for communication

**subnet mask**
- A subnet mask is a number that separates the host portion of an IP address from the network portion.

**DHCP**
- The acronym DHCP stands for Dynamic Host Configuration Protocol. It is a protocol used to provide quick, automatic, and central management for the distribution of IP addresses within a network.

**DNS**
- The term DNS stands out for Domain Name System, which is a system that converts human-readable website names into computer-readable numerical IP addresses.

**DNS server**
- A DNS (Domain Name System) server is a computer server that contains a database of public IP addresses and their associated hostnames. In addition, it is used to translate domain names (such as www.example.com) into IP addresses (such as 192.168.1.1).

**default gateway**
- A default gateway is a device on a network that acts as an access point or gateway for other devices in the network to communicate with the wider Internet.

**NAT**
- The acronym NAT stands out for Network Address Translation, which is a technology that is used to map a set of private IP addresses to a single public IP address.

**routing table**
- A routing table is a network-routing data structure that stores information about the paths that data packets take through a network. It generally contains some basic info, such as the destination and associated cost of each route

**port**
- A port is a communication endpoint used in networks for sending and receiving data. It is a logical construct that acts as a portal for allowing communication to and from a computer.

**packet**
- A packet is a unit of data sent over a network. It contains a header that includes source and destination addresses and other data, such as sequencing information and error-checking data.

**protocol**
- A protocol is a set of rules and conventions that govern the communication between two or more devices on a network, such as computers, routers, and servers. 

**bridge**
- A bridge in networking connects two or more network segments, managing the flow of data between them at the data link layer.

**NIC**
- The term NIC stands for Network Interface Card, which is technically a computer hardware component that allows a computer to connect to a network

**MAC address**
- A MAC (Media Access Control) address is a unique identifier assigned to a network interface controller (NIC) for communications on the physical network segment

**ARP**
- ARP stands for Address Resolution Protocol. In addition, it is a protocol used for mapping an IP address to a physical network address, such as a MAC address. 

**proxy server**
- A proxy server acts as an intermediary between a user's device and the internet. It receives requests from the user, forwards them to the internet, retrieves the responses, and then sends them back to the user. Proxy servers can be used for various purposes, including improving security, privacy, and performance, as well as bypassing content restrictions.

**DMZ**
- A DMZ (Demilitarized Zone) is a part of a computer network that is kept separate from the rest of the network, usually by a firewall. In addition, it is a secure area where external connections are allowed, but internal connections are blocked. This way, any attacks or malicious activity that may occur in the DMZ can be isolated and contained without affecting the rest of the network.

**NAC**
- The terminology NAC stands for Network Access Control, which is a system of hardware and software technologies used to control access to a computer network by enforcing various security policies. This is highly designed to ensure that only authorized users and devices can access the network. 

**NAS**
- The terminology NAS is the abbreviation for Network Attached Storage, which is a device that provides file-level data storage services to a network

**WLAN**
- The abbreviation WLAN stands for Wireless Local Area Network, which is a type of network that allows devices to connect to each other wirelessly. WLANs are commonly used in offices, homes, and public places such as airports and hotels.

**LAN extension**
- A LAN extension is a type of technology that enables users to extend the reach of their local area network (LAN) over a greater distance. In addition, it permits users to access the same network resources from remote locations as if they were directly connected to the LAN. 

**VTP**
- The acronym VTP abbreviates for Virtual Trunking Protocol, which is a Cisco proprietary protocol that is used to manage the configuration of trunk ports across a network of interconnected Cisco switches

**VLAN trunk**
- A VLAN trunk is a point-to-point link between two network devices that carries traffic for multiple VLANs. Technically, it is also known as a VLAN trunk port or 802.1Q trunk, which allows multiple VLANs to be carried over the same physical connection, allowing for the segmentation of a local area network (LAN).

**VLAN hopping**
- VLAN hopping is a type of attack in which an attacker is able to access traffic on a different VLAN than the one they are connected to. This type of network attack is when the attacker is able to gain access to a network or resources within a network that they should not have access to

**VLAN ID**
- A VLAN ID (virtual local area network identifier) is a number assigned to a VLAN in order to identify it on a network. In addition, it is used to segment a network into multiple logical networks and is typically used to separate different departments or functions in an organization.

**Switches:**
- Connect multiple devices in a network (Layer 2 devices).

**Hubs:**
- Connect computers over a network, transferring data between network devices.
- Operate at Layer 1 of the OSI model.

**Routers:**
- Connect one network to another via a modem, providing WiFi functionality.
- Operate at Layer 3 of the OSI model.

**Types of Switches:**
- KVM (Keyboard Video Mouse)
- Managed Switches: Require a network admin for monitoring and offer total control over network traffic.
- Unmanaged Switches: Plug-and-play devices with minimal installation beyond an Ethernet cable.
- Smart Switches: Managed devices with a limited set of management options.
- POE Switches: Distribute power over Ethernet to different devices.

**Manufacturers:**
- Netgear
- Cisco

**Address Formats:**
- **IPv6:** 128 bits
- **IPv4:** 32 bits
- **MAC (Media Access Control):** 48 bits

# Networking Concepts

- **Network:** A group of devices connected to each other.
- **Network Types:**
  - **PAN (Personal Area Network):** Communication between 2 devices (e.g., Bluetooth sharing).
  - **LAN (Local Area Network):** Privately owned network within a building, home, office, or library.
  - **MAN (Metropolitan Area Network):** Covers the entire city.
  - **WAN (Wide Area Network):** Spans a large geographical area, often a country or continent.
  - **GAN (Global Area Network):** Also known as the internet, connecting the globe using satellites.

- **VPN (Virtual Private Network):** Allows the creation of a secured tunnel between different networks using the internet.

- **Node:** Any communicating device in a network.
- **Link:** Connectivity between 2 nodes.
 
## Network Topology

The way devices are connected in a network.

### Types of Topology:

1. **Bus Topology:**
   - All devices are connected to a single cable called the bus.
   - Simple and inexpensive but susceptible to cable faults.

2. **Star Topology:**
   - All devices are connected to a central hub or switch.
   - Provides better performance and easier troubleshooting.

3. **Ring Topology:**
   - Each device is connected to two other devices, forming a ring.
   - Data travels in one direction around the ring.

4. **Mesh Topology:**
   - Each device is connected to every other device in the network.
   - Offers redundancy and fault tolerance but complex to manage.

5. **Hybrid Topology:**
   - Combination of two or more basic topologies.
   - Offers flexibility and scalability.

## IPv4 Address

IPv4 (Internet Protocol version 4) address is a numerical label assigned to devices connected to a network that uses the Internet Protocol for communication.

### Different Classes of IPv4:

1. **Class A:**
   - Starts with a 0 bit.
   - First octet ranges from 1 to 126.
   - Supports a large number of hosts but fewer networks.
   - Public IP range 1 to 127, Private IP range 10 to 10.255.255.255.

2. **Class B:**
   - Starts with a 10 bit.
   - First octet ranges from 128 to 191.
   - Supports moderate number of hosts and networks.
   - Public IP range 128 to 191, Private IP range 172.16.0.0 to 172.31.255.255.

3. **Class C:**
   - Starts with a 110 bit.
   - First octet ranges from 192 to 223.
   - Supports small number of hosts but large number of networks.
   - Public IP range 192 to 223, Private IP range 192.168.0.0 to 192.168.255.255.

4. **Class D:**
   - Starts with a 1110 bit.
   - Public IP range 224 to 239 used for multicasting.

5. **Class E:**
   - Starts with a 1111 bit.
   - Public IP range 240 to 255 reserved for research and experimental purposes.

## Private and Special IP Addresses

### Private IP Addresses:

Private IP addresses are reserved for use within private networks and are not directly accessible from the internet. They are commonly used for internal communication within an organization or home network. The three main ranges of private IP addresses specified by RFC 1918 are:

- **Class A Private IP Range:** 10.0.0.0 to 10.255.255.255 (10.0.0.0/8)
- **Class B Private IP Range:** 172.16.0.0 to 172.31.255.255 (172.16.0.0/12)
- **Class C Private IP Range:** 192.168.0.0 to 192.168.255.255 (192.168.0.0/16)

Devices within a private network can communicate with each other using these private IP addresses without requiring unique public IP addresses.

### Special IP Addresses:

Special IP addresses refer to specific addresses reserved for particular purposes. They include:

- **Loopback Address:** 127.0.0.1 (localhost), used by a device to send messages to itself.
- **Broadcast Address:** Typically the highest address in a subnet, used to send data to all devices within the subnet.
- **Link-local Addresses:** Used for communication within a single subnet and not routed outside the subnet. Example: 169.254.x.x addresses.
- **Multicast Addresses:** Used for one-to-many communication, where data is sent from one source to multiple recipients simultaneously. These addresses fall within the range 224.0.0.0 to 239.255.255.255.
- **Reserved Addresses:** Various addresses are reserved for future use or special purposes, such as 0.0.0.0, which typically represents an invalid or unknown target address, and 255.255.255.255, used for network broadcast on the local network segment.
