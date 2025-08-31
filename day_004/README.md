# Day 4: WAN Technologies

## Topics Covered
- WAN Technologies (Part 1)
- WAN Technologies (Part 2)
- WAN Technologies (Part 3)
- WAN Technologies (Part 4)

## 1. Introduction to Wide Area Networks (WANs)

A Wide Area Network (WAN) connects LANs across geographical distances, enabling communication between organizations, branch offices, and remote sites.

```mermaid
graph TD
    A[Wide Area Networks] --> B[Circuit-Switched]
    A --> C[Packet-Switched]
    A --> D[Cell-Switched]
    
    B --> B1[PSTN]
    B --> B2[ISDN]
    
    C --> C1[Frame Relay]
    C --> C2[X.25]
    C --> C3[MPLS]
    
    D --> D1[ATM]
    
    A --> E[Internet-Based]
    E --> E1[Broadband]
    E --> E2[DSL/Cable]
    E --> E3[Fiber]
    E --> E4[Satellite]
    E --> E5[Cellular]
```

## 2. Traditional WAN Technologies

### Leased Lines

Leased lines are dedicated point-to-point connections between two locations.

**Characteristics:**
- Dedicated bandwidth
- High reliability
- High cost
- Fixed capacity

**Types of Leased Lines:**
- T1/E1 (1.544/2.048 Mbps)
- T3/E3 (44.736/34.368 Mbps)
- OC-3, OC-12, OC-48, etc. (155 Mbps to 2.5 Gbps+)

```mermaid
graph LR
    A[Headquarters] -- Leased Line --- B[Branch Office]
```

### Frame Relay

Frame Relay is a packet-switching technology that operates at the data link layer (Layer 2).

**Key Concepts:**
- **PVC (Permanent Virtual Circuit)**: Predefined logical path between endpoints
- **DLCI (Data Link Connection Identifier)**: Identifies PVCs
- **CIR (Committed Information Rate)**: Guaranteed minimum bandwidth

```mermaid
graph TD
    A[Site A] --- FR[Frame Relay<br>Cloud]
    B[Site B] --- FR
    C[Site C] --- FR
    D[Site D] --- FR
    
    subgraph "Virtual Circuits"
    FR
    end
```

### Asynchronous Transfer Mode (ATM)

ATM is a cell-switching technology using fixed-size 53-byte cells.

**Characteristics:**
- Fixed cell size (53 bytes)
- Connection-oriented
- Quality of Service (QoS) support
- Virtual circuits

**ATM Service Categories:**
- CBR (Constant Bit Rate)
- VBR-rt (Variable Bit Rate - real time)
- VBR-nrt (Variable Bit Rate - non-real time)
- ABR (Available Bit Rate)
- UBR (Unspecified Bit Rate)

## 3. Modern WAN Technologies

### Multiprotocol Label Switching (MPLS)

MPLS is a routing technique that directs data using short path labels instead of long network addresses.

```mermaid
graph TD
    CE1[Customer Edge 1] --- PE1[Provider Edge 1]
    CE2[Customer Edge 2] --- PE2[Provider Edge 2]
    CE3[Customer Edge 3] --- PE3[Provider Edge 3]
    
    PE1 --- P1[Provider Core 1]
    PE1 --- P2[Provider Core 2]
    PE2 --- P2
    PE2 --- P3[Provider Core 3]
    PE3 --- P3
    PE3 --- P1
    
    subgraph "MPLS Network"
    PE1
    PE2
    PE3
    P1
    P2
    P3
    end
```

**MPLS Benefits:**
- Traffic engineering capabilities
- QoS support
- VPN support
- Protocol independence
- Improved performance

**MPLS VPN Types:**
- Layer 3 VPNs (IP VPNs)
- Layer 2 VPNs (VPWS, VPLS)

### Software-Defined WAN (SD-WAN)

SD-WAN is an application of software-defined networking (SDN) for WAN connections.

```mermaid
graph TD
    HQ[Headquarters] --- C[SD-WAN<br>Controller]
    
    HQ --- MPLS[MPLS]
    HQ --- INT1[Internet 1]
    HQ --- INT2[Internet 2]
    
    B1[Branch 1] --- MPLS
    B1 --- INT1
    
    B2[Branch 2] --- MPLS
    B2 --- INT2
    
    C -.- HQ
    C -.- B1
    C -.- B2
    
    classDef controller fill:#f9f,stroke:#333,stroke-width:2px;
    class C controller;
```

**SD-WAN Features:**
- Centralized control and management
- Dynamic path selection
- Application-aware routing
- Zero-touch provisioning
- Integrated security
- Cloud integration

**SD-WAN Benefits:**
- Lower cost compared to MPLS
- Improved application performance
- Simplified management
- Enhanced security
- Increased agility and flexibility

## 4. Internet-Based WAN Technologies

### Digital Subscriber Line (DSL)

DSL technology provides digital data transmission over telephone lines.

**DSL Types:**
- ADSL (Asymmetric DSL)
- SDSL (Symmetric DSL)
- VDSL (Very-high-bit-rate DSL)
- HDSL (High-bit-rate DSL)

**ADSL Connection Diagram:**
```mermaid
graph LR
    A[Customer Premises] --- B[DSLAM at CO]
    B --- C[ISP Network]
    C --- D[Internet]
    
    subgraph "Customer Site"
    A
    end
    
    subgraph "Service Provider"
    B
    C
    end
```

### Cable Broadband

Cable broadband uses the cable television infrastructure to provide internet access.

**Components:**
- CMTS (Cable Modem Termination System)
- Cable modem
- HFC (Hybrid Fiber-Coaxial) network

**Characteristics:**
- Shared medium (neighborhood)
- Higher download than upload speeds
- Bandwidth fluctuations during peak usage

### Fiber Optic Internet

Fiber optic internet uses light signals over fiber optic cables to transmit data.

**Types:**
- FTTH (Fiber to the Home)
- FTTB (Fiber to the Building)
- FTTC (Fiber to the Curb)

**Benefits:**
- Very high bandwidth (up to 10 Gbps)
- Low latency
- Long distance transmission
- Immune to electromagnetic interference

### Satellite Internet

Satellite internet provides connectivity via communications satellites.

**Types:**
- GEO (Geostationary Earth Orbit) - 35,786 km
- MEO (Medium Earth Orbit) - 2,000 to 35,786 km
- LEO (Low Earth Orbit) - 160 to 2,000 km

**Characteristics:**
- Global coverage, including remote areas
- Higher latency (especially for GEO)
- Weather sensitivity
- Improving speeds with new LEO constellations (Starlink, OneWeb)

## 5. WAN Connectivity Protocols

### Point-to-Point Protocol (PPP)

PPP is a data link protocol used to establish a direct connection between two nodes.

**PPP Components:**
- LCP (Link Control Protocol)
- NCP (Network Control Protocol)
- Authentication protocols (PAP, CHAP)

**PPP Frame Format:**
```
+------+------+------+-------------+------+
| Flag | Addr | Ctrl |    Data     | FCS  |
+------+------+------+-------------+------+
```

### PPP over Ethernet (PPPoE)

PPPoE combines Ethernet and PPP to provide authentication, encryption, and compression for Ethernet connections.

**PPPoE Process:**
1. Discovery stage (finds PPPoE server)
2. Session stage (establishes PPP session)

```mermaid
sequenceDiagram
    participant Client
    participant Server
    
    Client->>Server: PADI (PPPoE Active Discovery Initiation)
    Server->>Client: PADO (PPPoE Active Discovery Offer)
    Client->>Server: PADR (PPPoE Active Discovery Request)
    Server->>Client: PADS (PPPoE Active Discovery Session-confirmation)
    Note over Client,Server: PPP Session Established
    Client->>Server: PPP LCP Configuration
    Client->>Server: PPP Authentication
    Client->>Server: PPP NCP Configuration
    Note over Client,Server: Data Transfer
    Client->>Server: PADT (PPPoE Active Discovery Termination)
```

## 6. WAN Design Considerations

### Bandwidth Requirements

Calculate bandwidth needs based on:
- Number of users
- Application requirements
- Growth projections
- Peak usage patterns

**Bandwidth Calculation Example:**
```
Total bandwidth = (Number of users × Average usage per user) + Overhead
```

### Redundancy and Failover

Implement redundancy to ensure business continuity:

```mermaid
graph TD
    A[Headquarters] --- B[Primary WAN Link]
    A --- C[Backup WAN Link]
    B --- D[Branch Office]
    C --- D
```

**Redundancy Techniques:**
- Dual WAN connections
- Diverse routing paths
- Different service providers
- Automatic failover

### Quality of Service (QoS)

QoS techniques prioritize critical traffic:

**QoS Mechanisms:**
- Classification and marking
- Congestion management (queuing)
- Congestion avoidance
- Traffic policing and shaping
- Link efficiency mechanisms

**Traffic Classification:**
```
Voice > Video > Critical data > General data > Background
```

## 7. WAN Security

### Secure VPN Technologies

Virtual Private Networks (VPNs) create secure connections over public networks.

**VPN Types:**
- Site-to-Site VPNs
- Remote Access VPNs

```mermaid
graph TD
    A[Branch Office] --- V[VPN Tunnel] --- B[Headquarters]
    C[Remote User] --- V
    
    subgraph "Public Internet"
    V
    end
```

**VPN Protocols:**
- IPsec (Internet Protocol Security)
- SSL/TLS VPN
- PPTP (Point-to-Point Tunneling Protocol)
- L2TP/IPsec (Layer 2 Tunneling Protocol with IPsec)
- OpenVPN
- WireGuard

### WAN Encryption

Encryption protects data confidentiality over WAN links.

**Encryption Methods:**
- IPsec
- TLS/SSL
- MACsec (for Layer 2)

## Additional Resources

- [MPLS Architecture (RFC 3031)](https://tools.ietf.org/html/rfc3031)
- [PPP Protocol (RFC 1661)](https://tools.ietf.org/html/rfc1661)
- [Cisco SD-WAN Documentation](https://www.cisco.com/c/en/us/solutions/enterprise-networks/sd-wan/index.html)
- [IPsec VPN Design Considerations](https://www.cisco.com/c/en/us/support/docs/security-vpn/ipsec-negotiation-ike-protocols/14159-IPSec-part1.html)

## Practice Questions

1. Compare and contrast MPLS and SD-WAN technologies. When would you recommend each?
2. Design a redundant WAN solution for a company with headquarters and three branch offices.
3. Calculate the bandwidth requirements for a 100-user office where each user needs an average of 500 Kbps, voice traffic requires 2 Mbps, and video conferencing needs 10 Mbps.
4. Explain the PPPoE discovery process and why it's used in DSL connections.
