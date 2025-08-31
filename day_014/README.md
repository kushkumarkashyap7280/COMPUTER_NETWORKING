# Day 14: Network Security

## Topics Covered
- Network Security Fundamentals
- Security Devices and Solutions
- Cryptography and VPNs
- Security Policies and Best Practices

## 1. Introduction to Network Security

Network security consists of policies, practices, and technologies designed to protect network infrastructure, data, and communications from unauthorized access, misuse, malfunction, modification, destruction, or improper disclosure.

```mermaid
graph TD
    A[Network Security] --> B[Confidentiality]
    A --> C[Integrity]
    A --> D[Availability]
    A --> E[Authentication]
    A --> F[Authorization]
    A --> G[Accounting]
    
    B --> B1[Protecting sensitive information<br>from unauthorized access]
    C --> C1[Ensuring data is not altered<br>during transmission or storage]
    D --> D1[Systems and data available<br>when needed]
    E --> E1[Verifying identity of users<br>and systems]
    F --> F1[Determining what resources<br>users can access]
    G --> G1[Tracking user activities<br>and resource usage]
```

## 2. Network Security Threats

```mermaid
graph TD
    A[Network Security Threats] --> B[Malware]
    A --> C[Social Engineering]
    A --> D[Network Attacks]
    A --> E[Physical Threats]
    A --> F[Advanced Persistent Threats]
    
    B --> B1[Viruses]
    B --> B2[Worms]
    B --> B3[Trojans]
    B --> B4[Ransomware]
    B --> B5[Spyware]
    
    C --> C1[Phishing]
    C --> C2[Pretexting]
    C --> C3[Baiting]
    C --> C4[Tailgating]
    
    D --> D1[DoS/DDoS]
    D --> D2[Man-in-the-Middle]
    D --> D3[Packet Sniffing]
    D --> D4[IP Spoofing]
    D --> D5[ARP Poisoning]
    
    E --> E1[Theft]
    E --> E2[Unauthorized Access]
    E --> E3[Natural Disasters]
    
    F --> F1[Targeted attacks]
    F --> F2[Long-term presence]
    F --> F3[Multiple attack vectors]
```

### Malware

Malware (malicious software) is designed to damage, disrupt, or gain unauthorized access to systems.

**Types of Malware:**

- **Viruses**: Self-replicating malicious code that attaches to legitimate programs
- **Worms**: Self-replicating malware that spreads across networks without user interaction
- **Trojans**: Malware disguised as legitimate software
- **Ransomware**: Encrypts files and demands payment for decryption
- **Spyware**: Gathers information without consent
- **Rootkits**: Conceals presence and maintains privileged access
- **Keyloggers**: Records keystrokes to capture sensitive information
- **Adware**: Displays unwanted advertisements
- **Botnets**: Networks of compromised computers controlled remotely

### Social Engineering

Social engineering exploits human psychology to gain access to systems or information.

**Common Techniques:**

- **Phishing**: Fraudulent attempts to obtain sensitive information by impersonating trustworthy entities
- **Spear Phishing**: Targeted phishing attacks against specific individuals or organizations
- **Pretexting**: Creating a fabricated scenario to obtain information
- **Baiting**: Offering something enticing to entrap the victim
- **Tailgating**: Following someone to gain unauthorized physical access
- **Quid Pro Quo**: Offering a service in exchange for information
- **Vishing**: Voice phishing using phone calls

### Network Attacks

```mermaid
sequenceDiagram
    participant A as Attacker
    participant V1 as Victim 1
    participant V2 as Victim 2
    
    Note over A,V2: Man-in-the-Middle Attack
    V1->>A: Request to V2
    A->>V2: Modified Request
    V2->>A: Response to V1
    A->>V1: Modified Response
    
    Note over A,V2: Denial of Service Attack
    A->>V1: Flood of Requests
    Note over V1: Resources Exhausted
    V2->>V1: Legitimate Request
    Note over V1,V2: Connection Unavailable
```

**Common Network Attacks:**

- **Denial of Service (DoS)**: Overwhelms systems to prevent legitimate access
- **Distributed Denial of Service (DDoS)**: DoS from multiple sources
- **Man-in-the-Middle (MitM)**: Intercepts and potentially alters communications
- **Packet Sniffing**: Captures and analyzes network traffic
- **IP Spoofing**: Falsifies source IP address to impersonate another system
- **ARP Poisoning**: Corrupts ARP tables to redirect traffic
- **DNS Poisoning**: Corrupts DNS resolver cache to redirect traffic
- **Session Hijacking**: Takes over a valid user session
- **SQL Injection**: Attacks database through malicious SQL code
- **Cross-Site Scripting (XSS)**: Injects malicious scripts into web pages
- **Cross-Site Request Forgery (CSRF)**: Tricks users into executing unwanted actions

## 3. Network Security Devices and Solutions

### Firewalls

Firewalls monitor and control incoming and outgoing network traffic based on predetermined security rules.

```mermaid
graph TD
    A[Firewall Types] --> B[Packet Filtering Firewalls]
    A --> C[Stateful Inspection Firewalls]
    A --> D[Application Layer Firewalls]
    A --> E[Next-Generation Firewalls]
    A --> F[Web Application Firewalls]
    
    B --> B1[Examines packet headers<br>Based on access control lists]
    C --> C1[Tracks connection state<br>Context-aware filtering]
    D --> D1[Operates at Layer 7<br>Application-specific inspection]
    E --> E1[Deep packet inspection<br>Application awareness<br>Integrated IPS]
    F --> F1[Protects web applications<br>HTTP/HTTPS traffic monitoring]
```

**Firewall Deployment Models:**

```mermaid
graph TD
    A[Firewall Deployment] --> B[Network Firewall]
    A --> C[Host-Based Firewall]
    A --> D[Virtual Firewall]
    A --> E[Cloud Firewall]
    
    B --> B1[Protects network perimeter<br>Hardware appliance]
    C --> C1[Installed on individual hosts<br>Software-based]
    D --> D1[Deployed in virtualized environments<br>Protects virtual networks]
    E --> E1[Cloud-native security service<br>Protects cloud resources]
```

### Intrusion Detection and Prevention Systems

**Intrusion Detection System (IDS)**: Monitors network traffic for suspicious activity and issues alerts when detected.

**Intrusion Prevention System (IPS)**: Monitors network traffic like an IDS but can also take actions to prevent detected threats.

```mermaid
graph TD
    A[IDS/IPS Types] --> B[Network-Based NIDS/NIPS]
    A --> C[Host-Based HIDS/HIPS]
    A --> D[Wireless WIDS/WIPS]
    
    B --> B1[Monitors network traffic<br>Deployed at strategic points]
    C --> C1[Monitors host activities<br>Installed on endpoints]
    D --> D1[Monitors wireless networks<br>Detects rogue access points]
    
    E[Detection Methods] --> F[Signature-Based]
    E --> G[Anomaly-Based]
    E --> H[Behavior-Based]
    E --> I[Heuristic-Based]
    
    F --> F1[Matches known patterns<br>Requires regular updates]
    G --> G1[Detects deviations from normal<br>Baseline comparison]
    H --> H1[Identifies suspicious behaviors<br>Context-aware]
    I --> I1[Uses rules and algorithms<br>Pattern recognition]
```

### Network Access Control (NAC)

NAC enforces security policies on devices seeking to access network resources.

**Key Functions:**
- Pre-admission endpoint security checks
- Post-admission controls and monitoring
- Guest network access management
- IoT device security
- Compliance enforcement

**Implementation Types:**
- Agent-based
- Agentless
- Out-of-band
- Inline

### Security Information and Event Management (SIEM)

SIEM provides real-time analysis of security alerts generated by applications and network hardware.

**Capabilities:**
- Log collection and aggregation
- Correlation of events
- Alerting
- Dashboards and reporting
- Forensic analysis
- Compliance reporting

```mermaid
graph TD
    A[SIEM System] --> B[Log Collection]
    A --> C[Normalization]
    A --> D[Correlation Engine]
    A --> E[Analytics]
    A --> F[Alerting & Reporting]
    
    B --> B1[Network Devices]
    B --> B2[Servers]
    B --> B3[Applications]
    B --> B4[Security Devices]
    
    C --> C1[Standardizes log formats]
    
    D --> D1[Identifies relationships<br>between events]
    
    E --> E1[Detects anomalies<br>and patterns]
    
    F --> F1[Notifications]
    F --> F2[Dashboards]
    F --> F3[Reports]
```

### Web Security Gateway

Web security gateways filter unwanted software/malware from user-initiated web/internet traffic and enforce corporate and regulatory policy compliance.

**Features:**
- URL filtering
- Content inspection
- Malware scanning
- Data loss prevention
- Application control
- HTTPS inspection

### Email Security Gateway

Email security gateways protect against email-based threats.

**Capabilities:**
- Anti-spam filtering
- Anti-virus scanning
- Phishing protection
- Data loss prevention
- Email encryption
- Content filtering

## 4. Cryptography and VPNs

### Cryptography Fundamentals

Cryptography is the practice of secure communication in the presence of adversaries.

```mermaid
graph TD
    A[Cryptography Types] --> B[Symmetric Encryption]
    A --> C[Asymmetric Encryption]
    A --> D[Hash Functions]
    
    B --> B1[Single shared key<br>Faster processing]
    B --> B2[AES, DES, 3DES, Blowfish]
    
    C --> C1[Public/private key pairs<br>Slower than symmetric]
    C --> C2[RSA, ECC, DSA, Diffie-Hellman]
    
    D --> D1[One-way function<br>Fixed-length output]
    D --> D2[MD5, SHA-1, SHA-256, SHA-3]
```

**Encryption Process:**

```mermaid
sequenceDiagram
    participant S as Sender
    participant R as Recipient
    
    Note over S,R: Symmetric Encryption
    S->>S: Encrypt data with shared key
    S->>R: Send encrypted data
    R->>R: Decrypt with same shared key
    
    Note over S,R: Asymmetric Encryption
    S->>S: Encrypt data with recipient's public key
    S->>R: Send encrypted data
    R->>R: Decrypt with recipient's private key
    
    Note over S,R: Digital Signature
    S->>S: Create hash of data
    S->>S: Encrypt hash with sender's private key
    S->>R: Send data and digital signature
    R->>R: Decrypt signature with sender's public key
    R->>R: Verify hash matches data
```

### Public Key Infrastructure (PKI)

PKI is a framework for managing digital certificates and public-key encryption.

**Components:**
- Certificate Authority (CA)
- Registration Authority (RA)
- Certificate database
- Certificate store
- Key backup and recovery system

**Certificate Lifecycle:**
1. Certificate request
2. Verification and validation
3. Certificate issuance
4. Certificate distribution
5. Certificate revocation
6. Certificate expiration and renewal

### Virtual Private Networks (VPNs)

VPNs extend a private network across a public network, enabling users to send and receive data as if their devices were directly connected to the private network.

```mermaid
graph TD
    A[VPN Types] --> B[Remote Access VPNs]
    A --> C[Site-to-Site VPNs]
    A --> D[Mobile VPNs]
    A --> E[SSL/TLS VPNs]
    
    B --> B1[Individual user to network<br>Telecommuters, remote workers]
    C --> C1[Connects entire networks<br>Branch offices to headquarters]
    D --> D1[Maintains connection across<br>network transitions]
    E --> E2[Browser-based access<br>Clientless option]
    
    F[VPN Protocols] --> G[IPsec]
    F --> H[SSL/TLS]
    F --> I[OpenVPN]
    F --> J[L2TP/IPsec]
    F --> K[PPTP]
    F --> L[WireGuard]
    
    G --> G1[Authentication Header AH<br>Encapsulating Security Payload ESP]
    H --> H1[Transport Layer Security<br>Browser-compatible]
    I --> I1[Open-source<br>Highly configurable]
    J --> J1[Layer 2 tunneling<br>with IPsec encryption]
    K --> K1[Point-to-Point Tunneling<br>Less secure, legacy]
    L --> L1[Modern, high-performance<br>Simplified cryptography]
```

**IPsec VPN Modes:**

- **Transport Mode**: Encrypts only the payload/data portion of packets
- **Tunnel Mode**: Encrypts entire original packet

```mermaid
graph TD
    A[IPsec VPN Components] --> B[Internet Key Exchange IKE]
    A --> C[Authentication Header AH]
    A --> D[Encapsulating Security Payload ESP]
    A --> E[Security Associations SAs]
    
    B --> B1[Key management<br>Negotiates security parameters]
    C --> C1[Authentication<br>Integrity<br>Anti-replay]
    D --> D1[Encryption<br>Authentication<br>Integrity<br>Anti-replay]
    E --> E1[Security parameter database<br>Defines protection for traffic]
```

## 5. Network Security Policies and Best Practices

### Security Policies

```mermaid
graph TD
    A[Security Policy Framework] --> B[Acceptable Use Policy]
    A --> C[Access Control Policy]
    A --> D[Password Policy]
    A --> E[Network Security Policy]
    A --> F[Remote Access Policy]
    A --> G[Incident Response Policy]
    A --> H[Data Classification Policy]
    A --> I[Business Continuity Plan]
    A --> J[Disaster Recovery Plan]
```

**Policy Development Process:**
1. Risk assessment
2. Policy development
3. Review and approval
4. Implementation
5. Training and awareness
6. Monitoring and enforcement
7. Regular review and updates

### Defense in Depth

Defense in depth implements multiple layers of security controls throughout the IT environment.

```mermaid
graph TD
    A[Defense in Depth] --> B[Physical Security]
    A --> C[Perimeter Security]
    A --> D[Network Security]
    A --> E[Endpoint Security]
    A --> F[Application Security]
    A --> G[Data Security]
    
    B --> B1[Facility access controls<br>Environmental protections]
    C --> C1[Firewalls<br>DMZ<br>IDS/IPS]
    D --> D1[Network segmentation<br>Access controls<br>Traffic monitoring]
    E --> E1[Anti-malware<br>Host firewalls<br>Endpoint protection]
    F --> F1[Secure coding<br>Authentication<br>Patching]
    G --> G1[Encryption<br>Data loss prevention<br>Backup]
```

### Network Segmentation

Network segmentation divides a network into multiple segments or subnets, each acting as its own small network.

```mermaid
graph TD
    A[Network Segmentation] --> B[Physical Segmentation]
    A --> C[Logical Segmentation]
    A --> D[Micro-segmentation]
    
    B --> B1[Separate physical networks<br>Air-gapped systems]
    C --> C1[VLANs<br>Subnets<br>Routing]
    D --> D1[Fine-grained policies<br>Workload isolation<br>Zero trust model]
    
    E[Segmentation Models] --> F[Flat Network]
    E --> G[Traditional Segmentation]
    E --> H[Zero Trust Architecture]
    
    F --> F1[Single network segment<br>Limited internal controls]
    G --> G1[Perimeter-based<br>Trust zones<br>DMZ]
    H --> H1[No implicit trust<br>Verify every access<br>Least privilege]
```

**Benefits of Segmentation:**
- Limits attack surface
- Contains security breaches
- Protects sensitive data
- Reduces scope of compliance
- Improves performance

### Zero Trust Security

Zero Trust is a security framework that requires strict identity verification for every person and device trying to access resources, regardless of whether they are inside or outside the network perimeter.

```mermaid
graph TD
    A[Zero Trust Principles] --> B[Verify explicitly]
    A --> C[Use least privilege access]
    A --> D[Assume breach]
    
    B --> B1[Authentication<br>Authorization<br>Device validation]
    C --> C1[Just-in-time access<br>Just enough access<br>Risk-based adaptive policies]
    D --> D1[Minimize blast radius<br>Segment access<br>Encrypt data]
    
    E[Zero Trust Components] --> F[Identity Management]
    E --> G[Device Security]
    E --> H[Network Controls]
    E --> I[Application Security]
    E --> J[Data Protection]
    E --> K[Visibility and Analytics]
    
    F --> F1[MFA<br>Identity governance]
    G --> G1[Device health<br>Compliance state]
    H --> H1[Micro-segmentation<br>Software-defined perimeter]
    I --> I1[Application allowlisting<br>API security]
    J --> J1[Classification<br>Encryption<br>Rights management]
    K --> K1[Monitoring<br>Analytics<br>Automation]
```

### Security Monitoring and Incident Response

```mermaid
graph TD
    A[Security Operations] --> B[Continuous Monitoring]
    A --> C[Threat Hunting]
    A --> D[Vulnerability Management]
    A --> E[Incident Response]
    
    B --> B1[Log analysis<br>Alerts<br>Anomaly detection]
    C --> C1[Proactive searching<br>Threat intelligence<br>Behavioral analysis]
    D --> D1[Scanning<br>Assessment<br>Remediation]
    E --> E2[Preparation<br>Detection<br>Analysis<br>Containment<br>Eradication<br>Recovery<br>Lessons learned]
```

**Incident Response Process:**
1. **Preparation**: Develop IR plan, train team, prepare tools
2. **Detection**: Identify potential security incidents
3. **Analysis**: Investigate and confirm incidents
4. **Containment**: Isolate affected systems
5. **Eradication**: Remove malware, close vulnerabilities
6. **Recovery**: Restore systems to normal operation
7. **Lessons Learned**: Document findings, improve process

### Security Compliance and Standards

```mermaid
graph TD
    A[Security Standards] --> B[ISO/IEC 27001]
    A --> C[NIST Cybersecurity Framework]
    A --> D[PCI DSS]
    A --> E[HIPAA]
    A --> F[GDPR]
    A --> G[SOC 2]
    
    B --> B1[Information security management<br>Risk-based approach]
    C --> C1[Identify, Protect, Detect,<br>Respond, Recover]
    D --> D1[Payment card data security<br>12 requirements]
    E --> E1[Healthcare information<br>Privacy and security]
    F --> F1[Data protection and privacy<br>EU regulation]
    G --> G1[Service organization controls<br>Trust services criteria]
```

## 6. Network Security Best Practices

```mermaid
graph TD
    A[Security Best Practices] --> B[Regular Patching]
    A --> C[Strong Authentication]
    A --> D[Principle of Least Privilege]
    A --> E[Network Segmentation]
    A --> F[Regular Backups]
    A --> G[Security Awareness Training]
    A --> H[Asset Management]
    A --> I[Change Management]
    A --> J[Third-Party Risk Management]
    
    B --> B1[Operating systems<br>Applications<br>Firmware]
    C --> C1[Multi-factor authentication<br>Strong password policies]
    D --> D1[Minimum access needed<br>Regular access reviews]
    E --> E1[Separate sensitive systems<br>Control traffic flows]
    F --> F1[3-2-1 backup strategy<br>Regular testing]
    G --> G1[Phishing awareness<br>Security culture]
    H --> H1[Inventory management<br>Unauthorized device detection]
    I --> I1[Testing<br>Approval<br>Documentation]
    J --> J1[Vendor assessment<br>Contractual requirements]
```

**Specific Implementation Recommendations:**

- Implement multi-factor authentication (MFA) for all remote access
- Use network time protocol (NTP) for consistent timestamps
- Deploy centralized logging and monitoring
- Conduct regular vulnerability assessments and penetration testing
- Develop and test incident response and disaster recovery plans
- Encrypt sensitive data at rest and in transit
- Implement email and web content filtering
- Disable unnecessary services and ports
- Segment IoT devices from corporate networks
- Implement DNS filtering to block malicious domains

## Additional Resources

- [NIST Cybersecurity Framework](https://www.nist.gov/cyberframework)
- [SANS Internet Storm Center](https://isc.sans.edu/)
- [OWASP (Open Web Application Security Project)](https://owasp.org/)
- [US-CERT (United States Computer Emergency Readiness Team)](https://www.cisa.gov/us-cert)
- [Center for Internet Security (CIS)](https://www.cisecurity.org/)

## Practice Questions

1. Compare and contrast network-based and host-based intrusion detection systems. What are the advantages and limitations of each approach?

2. Explain the concept of defense in depth and how it can be implemented in a corporate network environment. Provide specific examples for each security layer.

3. A company is implementing a zero trust security model. Describe the key principles and components required for this implementation, and how it differs from traditional perimeter-based security.

4. Analyze the different types of VPN technologies and protocols. For a remote workforce scenario, which VPN solution would you recommend and why?

5. Describe the incident response process for handling a suspected ransomware attack. What immediate steps should be taken to contain the incident and minimize damage?
