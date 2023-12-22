# OSI Model

The OSI (Open Systems Interconnection) Model is a conceptual framework that standardizes the functions of a telecommunication or computing system into seven abstraction layers:

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

**User Datagram Protocol (UDP):**
- Sends data without confirming receipt or checking errors, which may result in some or all data being lost during transmission.
- Supports broadcasting.
- Ideal for live streaming, online gaming, and video chat.

# Networking Devices

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

# IP Addressing

- **Class A:** Public IP range 1 to 127, Private IP range 10 to 10.255.255.255.
- **Class B:** Public IP range 128 to 191, Private IP range 172.16.0.0 to 172.31.255.255.
- **Class C:** Public IP range 192 to 223, Private IP range 192.168.0.0 to 192.168.255.255.
- **Class D:** Public IP range 224 to 239 used for multicasting.
- **Class E:** Public IP range 240 to 255 reserved for research and experimental purposes.

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
- **Network Topology:** The way devices are connected in a network.