# Day 6: OSI Model and Protocol Architecture

<div align="center">
  <img src="https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExMW9wNWY5b29wMG42eGZuMTBsZ2pkZmt6Ymx2MXA0MnRwYTZ6amk0YyZlcD12MV9pbnRlcm5hbF9naWZzX2dpZklkJmN0PWc/3oKIPEqDGUULpEU0aQ/giphy.gif" width="500" alt="Network Layers Animation">
  
  <h1>🌐 The OSI Model and Protocol Architecture 🌐</h1>
  
  <p>
    <img src="https://img.shields.io/badge/OSI-7%20Layers-blue" alt="OSI">
    <img src="https://img.shields.io/badge/TCP%2FIP-4%20%26%205%20Layers-orange" alt="TCP/IP">
    <img src="https://img.shields.io/badge/Protocols-Multiple-green" alt="Protocols">
  </p>
  
  <hr>
</div>

## Table of Contents
- [Introduction to the OSI Model](#introduction-to-the-osi-model)
- [OSI Model Layers in Detail](#osi-model-layers-in-detail)
- [Protocols at Each Layer](#protocols-at-each-layer)
- [OSI vs TCP/IP Model](#osi-vs-tcpip-model)
  - [4-Layer TCP/IP Model](#4-layer-tcpip-model)
  - [5-Layer TCP/IP Model](#5-layer-tcpip-model)
- [Data Encapsulation and Decapsulation](#data-encapsulation-and-decapsulation)
- [Practice Questions](#practice-questions)

## Introduction to the OSI Model

The Open Systems Interconnection (OSI) model is a conceptual framework that standardizes the functions of a telecommunication or computing system without regard to its underlying internal structure and technology. Created by the International Organization for Standardization (ISO) in 1984, it provides a common basis for coordinating standards development for the purpose of systems interconnection.

### The Need for a Layered Model

```mermaid
graph TD
    A[Problem: Complex Networking Tasks] --> B[Solution: Divide into Smaller Manageable Layers]
    B --> C[Benefits: Standardization]
    B --> D[Benefits: Modularity]
    B --> E[Benefits: Easier Troubleshooting]
    B --> F[Benefits: Parallel Development]
```

## OSI Model Layers in Detail

### Complete OSI Model Overview

```mermaid
graph TB
    subgraph "OSI Model"
        L7[Layer 7: Application]
        L6[Layer 6: Presentation]
        L5[Layer 5: Session]
        L4[Layer 4: Transport]
        L3[Layer 3: Network]
        L2[Layer 2: Data Link]
        L1[Layer 1: Physical]
    end
    
    L7 --> L6
    L6 --> L5
    L5 --> L4
    L4 --> L3
    L3 --> L2
    L2 --> L1
    
    subgraph "Data Units"
        D7[Data]
        D6[Data]
        D5[Data]
        D4[Segments/Datagrams]
        D3[Packets]
        D2[Frames]
        D1[Bits]
    end
    
    L7 -.-> D7
    L6 -.-> D6
    L5 -.-> D5
    L4 -.-> D4
    L3 -.-> D3
    L2 -.-> D2
    L1 -.-> D1
```

### Layer 7: Application Layer

```mermaid
graph LR
    A[Application Layer] --> B[User Interface]
    A --> C[Resource Sharing]
    A --> D[Remote File Access]
    A --> E[Directory Services]
    A --> F[Email Services]
```

**Function**: Provides network services directly to end-users or applications.

**Protocols**:
- HTTP/HTTPS (Web browsing)
- SMTP/POP3/IMAP (Email)
- FTP/SFTP (File transfer)
- DNS (Domain name resolution)
- DHCP (Dynamic host configuration)
- Telnet/SSH (Remote access)
- SNMP (Network management)

**One Line Function**: Provides network services to applications and directly interacts with end-users.

### Layer 6: Presentation Layer

```mermaid
graph LR
    A[Presentation Layer] --> B[Data Translation]
    A --> C[Encryption/Decryption]
    A --> D[Compression/Decompression]
    A --> E[Format Conversion]
```

**Function**: Translates data between the application layer and lower layers. Handles data formatting, encryption, and compression.

**Protocols**:
- SSL/TLS (Encryption)
- JPEG, GIF, PNG (Image formats)
- MPEG, MP4 (Video formats)
- ASCII, EBCDIC (Character encoding)
- XML, JSON (Data structures)

**One Line Function**: Transforms data into a format that the application layer can accept or that can be sent over the network.

### Layer 5: Session Layer

```mermaid
graph LR
    A[Session Layer] --> B[Session Establishment]
    A --> C[Session Maintenance]
    A --> D[Session Termination]
    A --> E[Authentication]
    A --> F[Synchronization]
```

**Function**: Establishes, manages, and terminates sessions between applications.

**Protocols**:
- NetBIOS (Network Basic Input/Output System)
- RPC (Remote Procedure Call)
- SIP (Session Initiation Protocol)
- SQL (Structured Query Language)
- NFS (Network File System)

**One Line Function**: Manages the communication sessions between computers, including establishing, maintaining, and terminating connections.

### Layer 4: Transport Layer

```mermaid
graph LR
    A[Transport Layer] --> B[End-to-End Communication]
    A --> C[Reliability]
    A --> D[Flow Control]
    A --> E[Error Recovery]
    A --> F[Segmentation and Reassembly]
    
    subgraph "TCP vs UDP"
        TCP[TCP: Connection-oriented, Reliable]
        UDP[UDP: Connectionless, Fast]
    end
```

**Function**: Provides reliable data transfer, segmentation, flow control, and error correction.

**Protocols**:
- TCP (Transmission Control Protocol)
- UDP (User Datagram Protocol)
- SCTP (Stream Control Transmission Protocol)
- DCCP (Datagram Congestion Control Protocol)

**One Line Function**: Ensures complete data transfer by managing flow control, error correction, and data segmentation.

### Layer 3: Network Layer

```mermaid
graph LR
    A[Network Layer] --> B[Logical Addressing]
    A --> C[Path Determination]
    A --> D[Routing]
    A --> E[Packet Forwarding]
    A --> F[Fragmentation and Reassembly]
    
    subgraph "IP Addressing"
        IP4[IPv4: 32-bit]
        IP6[IPv6: 128-bit]
    end
```

**Function**: Handles logical addressing, routing, and path determination.

**Protocols**:
- IPv4/IPv6 (Internet Protocol)
- ICMP (Internet Control Message Protocol)
- IGMP (Internet Group Management Protocol)
- RIP, OSPF, BGP (Routing protocols)
- IPsec (IP Security)
- MPLS (Multiprotocol Label Switching)

**One Line Function**: Determines the best path for data to travel from source to destination across multiple networks.

### Layer 2: Data Link Layer

```mermaid
graph TB
    A[Data Link Layer] --> B[MAC Addressing]
    A --> C[Frame Traffic Control]
    A --> D[Error Detection/Correction]
    
    subgraph "Sublayers"
        MAC[Media Access Control - MAC]
        LLC[Logical Link Control - LLC]
    end
    
    B --> MAC
    C --> LLC
    D --> LLC
```

**Function**: Provides node-to-node data transfer and handles physical addressing, error detection, and frame flow control.

**Protocols**:
- Ethernet (IEEE 802.3)
- Wi-Fi (IEEE 802.11)
- PPP (Point-to-Point Protocol)
- HDLC (High-Level Data Link Control)
- ATM (Asynchronous Transfer Mode)
- Frame Relay
- Bluetooth (IEEE 802.15)

**One Line Function**: Creates and maintains reliable links between directly connected nodes by managing physical addressing and access to the medium.

### Layer 1: Physical Layer

```mermaid
graph LR
    A[Physical Layer] --> B[Bit Transmission]
    A --> C[Physical Connections]
    A --> D[Topology]
    A --> E[Transmission Mode]
    
    subgraph "Physical Media"
        Copper[Copper Cable]
        Fiber[Fiber Optic]
        Wireless[Wireless Media]
    end
```

**Function**: Transmits raw bit streams over a physical medium.

**Protocols/Standards**:
- RS-232, RS-449 (Serial interfaces)
- DSL (Digital Subscriber Line)
- ISDN (Integrated Services Digital Network)
- USB (Universal Serial Bus)
- Bluetooth Physical Layer
- IEEE 802.11 Physical Layer
- SONET/SDH (Synchronous Optical Networking)

**One Line Function**: Transmits and receives raw bit streams over a physical medium, dealing with cables, pins, voltages, and signal modulation.

## Protocols at Each Layer

```mermaid
graph TB
    subgraph "Application Layer (7)"
        HTTP
        FTP
        SMTP
        DNS
        DHCP
        Telnet
        SSH
    end
    
    subgraph "Presentation Layer (6)"
        SSL/TLS
        JPEG/GIF/PNG
        MPEG
        ASCII
        XML/JSON
    end
    
    subgraph "Session Layer (5)"
        NetBIOS
        RPC
        SIP
        SQL
        NFS
    end
    
    subgraph "Transport Layer (4)"
        TCP
        UDP
        SCTP
        DCCP
    end
    
    subgraph "Network Layer (3)"
        IPv4/IPv6
        ICMP
        IGMP
        RIP/OSPF/BGP
        IPsec
    end
    
    subgraph "Data Link Layer (2)"
        Ethernet
        WiFi
        PPP
        HDLC
        ATM
    end
    
    subgraph "Physical Layer (1)"
        RS232
        DSL
        ISDN
        USB
        802.11
    end
```

## OSI vs TCP/IP Model

There are two common representations of the TCP/IP model: the original 4-layer model and the more detailed 5-layer model. Both simplify the OSI model while providing practical frameworks for internet communications.

### 4-Layer TCP/IP Model

The original TCP/IP model has 4 layers and maps to the OSI model as follows:

```mermaid
graph LR
    subgraph "OSI Model"
        O7[Application]
        O6[Presentation]
        O5[Session]
        O4[Transport]
        O3[Network]
        O2[Data Link]
        O1[Physical]
    end
    
    subgraph "4-Layer TCP/IP Model"
        T4[Application]
        T3[Transport]
        T2[Internet]
        T1[Network Interface]
    end
    
    O7 --> T4
    O6 --> T4
    O5 --> T4
    O4 --> T3
    O3 --> T2
    O2 --> T1
    O1 --> T1
```

### 5-Layer TCP/IP Model

The 5-layer TCP/IP model is more commonly used in educational contexts and provides clearer distinctions between the physical and data link layers:

```mermaid
graph LR
    subgraph "OSI Model"
        O7[Application]
        O6[Presentation]
        O5[Session]
        O4[Transport]
        O3[Network]
        O2[Data Link]
        O1[Physical]
    end
    
    subgraph "5-Layer TCP/IP Model"
        T5[Application]
        T4[Transport]
        T3[Network/Internet]
        T2[Data Link]
        T1[Physical]
    end
    
    O7 --> T5
    O6 --> T5
    O5 --> T5
    O4 --> T4
    O3 --> T3
    O2 --> T2
    O1 --> T1
```

### 5-Layer TCP/IP Model in Detail

```mermaid
graph TB
    subgraph "5-Layer TCP/IP Model"
        L5[Layer 5: Application]
        L4[Layer 4: Transport]
        L3[Layer 3: Network/Internet]
        L2[Layer 2: Data Link]
        L1[Layer 1: Physical]
    end
    
    L5 --> L4
    L4 --> L3
    L3 --> L2
    L2 --> L1
    
    subgraph "Protocols"
        P5[HTTP, FTP, SMTP, DNS, Telnet]
        P4[TCP, UDP]
        P3[IP, ICMP, ARP, IGMP]
        P2[Ethernet, PPP, HDLC]
        P1[RS-232, Ethernet, Wi-Fi Physical]
    end
    
    L5 -.-> P5
    L4 -.-> P4
    L3 -.-> P3
    L2 -.-> P2
    L1 -.-> P1
    
    subgraph "PDUs"
        D5[Data]
        D4[Segment/Datagram]
        D3[Packet]
        D2[Frame]
        D1[Bit]
    end
    
    L5 -.-> D5
    L4 -.-> D4
    L3 -.-> D3
    L2 -.-> D2
    L1 -.-> D1
```

#### Layer 5: Application Layer
- **Function**: Provides network services to applications
- **Protocols**: HTTP, HTTPS, FTP, SMTP, DNS, Telnet, SSH, SNMP
- **PDU**: Data
- **Combines**: OSI Application, Presentation, and Session layers

#### Layer 4: Transport Layer
- **Function**: End-to-end communication, reliability, flow control
- **Protocols**: TCP, UDP
- **PDU**: Segment (TCP) / Datagram (UDP)
- **Maps to**: OSI Transport layer

#### Layer 3: Network/Internet Layer
- **Function**: Logical addressing, routing between networks
- **Protocols**: IP (IPv4, IPv6), ICMP, ARP, IGMP, Routing protocols
- **PDU**: Packet
- **Maps to**: OSI Network layer

#### Layer 2: Data Link Layer
- **Function**: Physical addressing, local network access
- **Protocols**: Ethernet, PPP, HDLC, Wi-Fi
- **PDU**: Frame
- **Maps to**: OSI Data Link layer

#### Layer 1: Physical Layer
- **Function**: Bit transmission, physical connections
- **Standards**: RS-232, Ethernet physical, Wi-Fi physical, USB
- **PDU**: Bit
- **Maps to**: OSI Physical layer

### Key Differences Between Models

| OSI Model | 4-Layer TCP/IP | 5-Layer TCP/IP | Main Functions |
|-----------|----------------|----------------|---------------|
| Application, Presentation, Session | Application | Application | User interfaces, data encoding, session management |
| Transport | Transport | Transport | End-to-end communication, reliability |
| Network | Internet | Network/Internet | Logical addressing, routing |
| Data Link | Network Interface | Data Link | Physical addressing, medium access |
| Physical | Network Interface | Physical | Bit transmission, cabling, signals |

## Data Encapsulation and Decapsulation

As data travels down the OSI model from sender to receiver, each layer adds its own header (and sometimes trailer) to the data. This process is called encapsulation. The reverse process, as data moves up the layers at the receiving end, is called decapsulation.

```mermaid
graph TB
    subgraph "Sender"
        S7[Application Data]
        S6[+ Presentation Header]
        S5[+ Session Header]
        S4[+ Transport Header]
        S3[+ Network Header]
        S2[+ Data Link Header/Trailer]
        S1[Physical Bits]
    end
    
    S7 --> S6
    S6 --> S5
    S5 --> S4
    S4 --> S3
    S3 --> S2
    S2 --> S1
    
    S1 --> R1
    
    subgraph "Receiver"
        R1[Physical Bits]
        R2[- Data Link Header/Trailer]
        R3[- Network Header]
        R4[- Transport Header]
        R5[- Session Header]
        R6[- Presentation Header]
        R7[Application Data]
    end
    
    R1 --> R2
    R2 --> R3
    R3 --> R4
    R4 --> R5
    R5 --> R6
    R6 --> R7
```

### Protocol Data Units (PDUs)

Each layer in the OSI model has a specific name for the data unit it handles:

| Layer | PDU Name |
|-------|----------|
| Application | Data |
| Presentation | Data |
| Session | Data |
| Transport | Segment (TCP) / Datagram (UDP) |
| Network | Packet |
| Data Link | Frame |
| Physical | Bit |

## Practice Questions

1. Explain the purpose of the OSI model and why a layered approach is beneficial for networking.

2. If you were troubleshooting a network issue where two computers on the same network couldn't communicate, which OSI layers would you investigate first and why?

3. Compare and contrast TCP and UDP at the Transport layer. In what scenarios would you choose one over the other?

4. How does encapsulation work as data moves down the OSI model? What information is typically added at each layer?

5. Match the following protocols to their correct OSI layer:
   - HTTPS
   - IPv6
   - Ethernet
   - TCP
   - SSL

6. Explain the difference between logical addressing (Layer 3) and physical addressing (Layer 2).

7. What happens at the Physical layer when a message is transmitted over a wireless network versus a wired network?

8. How does the Session layer establish, manage, and terminate connections?

9. What role does the Presentation layer play in ensuring different systems can understand each other's data formats?

10. Draw a simple diagram showing how data flows through the OSI layers when a web browser requests a webpage from a server.

## Additional Resources

- [Interactive OSI Model Simulator](https://www.gns3.com/)
- [Wireshark: Protocol Analyzer](https://www.wireshark.org/)
- [RFC 1122: Requirements for Internet Hosts](https://tools.ietf.org/html/rfc1122)
- [Book: Computer Networks by Andrew S. Tanenbaum](https://www.amazon.com/Computer-Networks-5th-Andrew-Tanenbaum/dp/0132126958)

---

<div align="center">
  <p>
    <a href="../day_005/README.md">⬅️ Previous Day</a> | 
    <a href="../README.md">🏠 Home</a> |
    <a href="../day_007/README.md">➡️ Next Day</a>
  </p>
</div>
