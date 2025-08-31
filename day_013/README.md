# Day 13: Cloud Computing & SDN

## Topics Covered
- Cloud Computing
- Software-Defined Networking (SDN)

## 1. Introduction to Cloud Computing

Cloud computing is a model for enabling ubiquitous, convenient, on-demand network access to a shared pool of configurable computing resources that can be rapidly provisioned and released with minimal management effort or service provider interaction.

```mermaid
graph TD
    A[Cloud Computing] --> B[Service Models]
    A --> C[Deployment Models]
    A --> D[Essential Characteristics]
    
    B --> B1[Infrastructure as a Service IaaS]
    B --> B2[Platform as a Service PaaS]
    B --> B3[Software as a Service SaaS]
    
    C --> C1[Public Cloud]
    C --> C2[Private Cloud]
    C --> C3[Hybrid Cloud]
    C --> C4[Community Cloud]
    
    D --> D1[On-demand Self-service]
    D --> D2[Broad Network Access]
    D --> D3[Resource Pooling]
    D --> D4[Rapid Elasticity]
    D --> D5[Measured Service]
```

## 2. Cloud Service Models

### Infrastructure as a Service (IaaS)

IaaS provides virtualized computing resources over the internet, including virtual machines, storage, and networking.

**Key Characteristics:**
- Compute resources provided as a service
- Dynamic scaling of resources
- Pay-as-you-go pricing model
- Self-service provisioning
- Managed infrastructure

**Examples:**
- Amazon EC2
- Microsoft Azure Virtual Machines
- Google Compute Engine
- IBM Cloud
- DigitalOcean Droplets

```mermaid
graph TD
    A[IaaS Components] --> B[Compute]
    A --> C[Storage]
    A --> D[Networking]
    A --> E[Security]
    
    B --> B1[Virtual Machines]
    B --> B2[Containers]
    B --> B3[Bare Metal Servers]
    
    C --> C1[Block Storage]
    C --> C2[Object Storage]
    C --> C3[File Storage]
    
    D --> D1[Virtual Networks]
    D --> D2[Load Balancers]
    D --> D3[VPN]
    D --> D4[Firewalls]
    
    E --> E1[Identity Management]
    E --> E2[Access Controls]
    E --> E3[Encryption]
```

**User Responsibilities:**
- Operating systems
- Applications
- Data
- Runtime
- Middleware

### Platform as a Service (PaaS)

PaaS provides a platform allowing customers to develop, run, and manage applications without the complexity of building and maintaining the infrastructure.

**Key Characteristics:**
- Development tools, database management systems, business analytics
- Ready-to-use development environment
- Integrated deployment, testing, and hosting
- Automatic scaling and high availability
- API integration and middleware

**Examples:**
- Google App Engine
- Microsoft Azure App Service
- AWS Elastic Beanstalk
- Heroku
- IBM Cloud Foundry

```mermaid
graph TD
    A[PaaS Components] --> B[Development Tools]
    A --> C[Database Services]
    A --> D[Application Hosting]
    A --> E[Integration Services]
    
    B --> B1[IDEs]
    B --> B2[SDKs]
    B --> B3[API Management]
    
    C --> C1[Relational Databases]
    C --> C2[NoSQL Databases]
    C --> C3[Caching Services]
    
    D --> D1[Web Servers]
    D --> D2[Application Containers]
    D --> D3[Runtime Environments]
    
    E --> E1[API Gateways]
    E --> E2[Message Queues]
    E --> E3[Event Streaming]
```

**User Responsibilities:**
- Applications
- Data

### Software as a Service (SaaS)

SaaS delivers software applications over the internet, on a subscription basis, centrally hosted and managed by the service provider.

**Key Characteristics:**
- Web-based access to commercial software
- Applications managed from a central location
- One-to-many delivery model
- Automatic updates
- Subscription-based pricing

**Examples:**
- Microsoft 365
- Google Workspace
- Salesforce
- Dropbox
- Slack

```mermaid
graph TD
    A[SaaS Applications] --> B[Productivity]
    A --> C[Collaboration]
    A --> D[Business Operations]
    A --> E[Customer Management]
    
    B --> B1[Office Suites]
    B --> B2[Email]
    B --> B3[Calendar]
    
    C --> C1[File Sharing]
    C --> C2[Communication Tools]
    C --> C3[Project Management]
    
    D --> D1[ERP]
    D --> D2[Finance]
    D --> D3[HR Systems]
    
    E --> E1[CRM]
    E --> E2[Marketing Automation]
    E --> E3[Customer Support]
```

**User Responsibilities:**
- Data
- Access management

### Function as a Service (FaaS)

FaaS is a type of cloud computing service that allows developers to execute code in response to events without managing the underlying infrastructure.

**Key Characteristics:**
- Event-driven execution
- Stateless functions
- Automatic scaling
- Pay only for execution time
- No server management

**Examples:**
- AWS Lambda
- Azure Functions
- Google Cloud Functions
- IBM Cloud Functions
- Cloudflare Workers

## 3. Cloud Deployment Models

### Public Cloud

Public cloud services are delivered over the public internet and shared across organizations.

**Characteristics:**
- Owned and operated by third-party providers
- Available to general public
- Multi-tenant architecture
- Elastic, on-demand resources
- Pay-as-you-go pricing

**Examples:**
- Amazon Web Services (AWS)
- Microsoft Azure
- Google Cloud Platform (GCP)
- IBM Cloud
- Oracle Cloud

### Private Cloud

Private cloud is dedicated solely to a single organization, either managed internally or by a third party.

**Characteristics:**
- Single-tenant environment
- Greater control and customization
- Enhanced security and privacy
- Compliance advantages
- Predictable performance

**Implementation Options:**
- On-premises private cloud
- Hosted private cloud
- Virtual private cloud (VPC)

### Hybrid Cloud

Hybrid cloud combines public and private clouds, allowing data and applications to be shared between them.

```mermaid
graph LR
    A[Hybrid Cloud] --- B[Private Cloud]
    A --- C[Public Cloud]
    
    B --- B1[On-premises<br>Data Center]
    B --- B2[Hosted Private<br>Cloud]
    
    C --- C1[Public Cloud<br>Services]
    
    B1 --- D[Integration Layer]
    B2 --- D
    C1 --- D
    
    D --- E1[Cloud Management<br>Platform]
    D --- E2[Network<br>Connectivity]
    D --- E3[Identity<br>Management]
```

**Characteristics:**
- Workload flexibility
- Data sovereignty
- Cost optimization
- Scalability with security
- Gradual cloud migration

**Examples:**
- AWS Outposts + AWS public cloud
- Azure Stack + Azure public cloud
- Google Anthos
- IBM Cloud Satellite

### Community Cloud

Community cloud infrastructure is shared among several organizations with common concerns (security, compliance, jurisdiction).

**Characteristics:**
- Shared infrastructure
- Cost sharing among community
- Compliance with industry regulations
- Collaborative governance
- Common security requirements

**Examples:**
- Government clouds
- Healthcare clouds
- Financial services clouds
- Education clouds

## 4. Cloud Computing Benefits and Challenges

### Benefits

```mermaid
graph TD
    A[Cloud Benefits] --> B[Cost Efficiency]
    A --> C[Scalability]
    A --> D[Flexibility]
    A --> E[Reliability]
    A --> F[Performance]
    A --> G[Security]
    
    B --> B1[Reduced CapEx<br>Pay-as-you-go]
    C --> C1[Elastic resources<br>Auto-scaling]
    D --> D1[Device/location<br>independence]
    E --> E1[High availability<br>Disaster recovery]
    F --> F1[Global data centers<br>Edge computing]
    G --> G1[Dedicated security<br>Regular updates]
```

### Challenges

```mermaid
graph TD
    A[Cloud Challenges] --> B[Security & Privacy]
    A --> C[Compliance]
    A --> D[Integration]
    A --> E[Vendor Lock-in]
    A --> F[Cost Management]
    A --> G[Performance]
    
    B --> B1[Data breaches<br>Shared infrastructure]
    C --> C1[Regulatory requirements<br>Data sovereignty]
    D --> D1[Legacy systems<br>API compatibility]
    E --> E1[Proprietary technologies<br>Migration difficulties]
    F --> F1[Hidden costs<br>Resource optimization]
    G --> G1[Latency<br>Network limitations]
```

## 5. Cloud Network Concepts

### Virtual Private Cloud (VPC)

A VPC is a logically isolated section of the public cloud where you can launch resources in a virtual network that you define.

```mermaid
graph TD
    A[Virtual Private Cloud] --- B[Subnets]
    A --- C[Route Tables]
    A --- D[Internet Gateway]
    A --- E[Security Groups]
    A --- F[Network ACLs]
    
    B --- B1[Public Subnet]
    B --- B2[Private Subnet]
    
    B1 --- G[Web Servers]
    B2 --- H[Database Servers]
    
    D --- I[Internet]
    G --- D
```

**Key Components:**
- Subnets: Public and private
- Route tables: Control traffic flow
- Internet gateway: Provides internet access
- NAT gateway: Allows private subnet outbound traffic
- Security groups: Firewall for instances
- Network ACLs: Stateless subnet-level security

### Cloud Networking Services

```mermaid
graph TD
    A[Cloud Networking Services] --> B[Load Balancing]
    A --> C[Content Delivery Network CDN]
    A --> D[DNS Services]
    A --> E[Direct Connect/ExpressRoute]
    A --> F[VPN Connectivity]
    A --> G[Transit Gateway/VPC Peering]
    
    B --> B1[Application Load Balancers]
    B --> B2[Network Load Balancers]
    B --> B3[Global Load Balancers]
    
    C --> C1[Edge Locations]
    C --> C2[Content Caching]
    C --> C3[Media Streaming]
    
    D --> D1[Managed DNS]
    D --> D2[Traffic Routing]
    D --> D3[Health Checks]
    
    E --> E1[Dedicated Connections]
    E --> E2[Partner Connections]
    
    F --> F1[Site-to-Site VPN]
    F --> F2[Client VPN]
    
    G --> G1[Inter-VPC Networking]
    G --> G2[Regional Connectivity]
```

## 6. Software-Defined Networking (SDN)

SDN is an approach to networking that uses software-based controllers or application programming interfaces (APIs) to communicate with underlying hardware infrastructure and direct traffic on a network.

```mermaid
graph TD
    A[Traditional Networking] --> B[Control Plane + Data Plane<br>Integrated in Network Devices]
    
    C[Software-Defined Networking] --> D[Control Plane]
    C --> E[Data Plane]
    
    D --> F[Centralized Controller]
    F --> G[Network Applications]
    F --> H[APIs]
    
    E --> I[Network Devices]
    H --> I
```

### SDN Architecture

```mermaid
graph TD
    A[SDN Architecture] --> B[Application Layer]
    A --> C[Control Layer]
    A --> D[Infrastructure Layer]
    
    B --- C
    C --- D
    
    B --> B1[Network Applications<br>and Services]
    C --> C1[SDN Controller]
    D --> D1[Network Devices<br>Physical and Virtual]
    
    C1 --- C2[Northbound APIs]
    C1 --- C3[Southbound APIs<br>OpenFlow, NETCONF]
```

**Application Layer:**
- Business applications
- Network services (firewalls, load balancing)
- Orchestration tools
- Uses northbound APIs to communicate with the control layer

**Control Layer:**
- SDN controller(s)
- Network state information
- Policy management
- Uses southbound APIs to communicate with infrastructure

**Infrastructure Layer:**
- Physical and virtual switches/routers
- Packet forwarding
- Data path functions
- Exposes capabilities via southbound APIs

### SDN Controllers

SDN controllers provide a centralized view of the overall network and enable administrators to dictate to the underlying systems how the forwarding plane should handle network traffic.

**Examples:**
- OpenDaylight
- ONOS (Open Network Operating System)
- VMware NSX
- Cisco ACI
- Juniper Contrail

### SDN Protocols

**OpenFlow:**
The first standard communication interface defined between the control and forwarding layers of an SDN architecture.

**OpenFlow Operations:**
- Controller-to-switch messages
- Asynchronous messages
- Symmetric messages
- Flow table programming

```mermaid
sequenceDiagram
    participant Controller
    participant Switch
    
    Controller->>Switch: Flow rule installation
    Switch->>Controller: Flow table status
    
    Note over Controller,Switch: New flow packet arrival
    Switch->>Controller: Packet-in message
    Controller->>Switch: Flow rule installation
    Switch->>Controller: Acknowledgment
```

**Other SDN Protocols:**
- NETCONF/YANG
- OVSDB (Open vSwitch Database Management Protocol)
- P4 (Programming Protocol-independent Packet Processors)
- gRPC/gNMI

### SDN Benefits

```mermaid
graph TD
    A[SDN Benefits] --> B[Centralized Management]
    A --> C[Network Programmability]
    A --> D[Service Agility]
    A --> E[Network Abstraction]
    A --> F[Hardware Independence]
    A --> G[Automation]
    
    B --> B1[Single control point<br>Simplified operations]
    C --> C1[Programmatic interface<br>API-driven configuration]
    D --> D1[Rapid service deployment<br>Dynamic provisioning]
    E --> E1[Logical network control<br>Independent of hardware]
    F --> F1[Vendor neutrality<br>White-box switching]
    G --> G1[Reduced manual tasks<br>Policy-based management]
```

### SDN Use Cases

```mermaid
graph TD
    A[SDN Use Cases] --> B[Data Center Networking]
    A --> C[Cloud Computing]
    A --> D[Network Function Virtualization]
    A --> E[Campus/Enterprise Networks]
    A --> F[WAN Optimization]
    A --> G[Security Services]
    
    B --> B1[Fabric management<br>Multi-tenant networks]
    C --> C1[Elastic resource allocation<br>Network virtualization]
    D --> D1[Service chaining<br>Virtual network functions]
    E --> E1[Policy enforcement<br>Access control]
    F --> F1[Traffic engineering<br>SD-WAN]
    G --> G1[Micro-segmentation<br>DDoS mitigation]
```

## 7. Network Function Virtualization (NFV)

NFV decouples network functions from proprietary hardware appliances and runs them as software on standard servers.

```mermaid
graph TD
    A[NFV Architecture] --> B[NFV Infrastructure NFVI]
    A --> C[Virtual Network Functions VNFs]
    A --> D[NFV Management and Orchestration MANO]
    
    B --> B1[Compute]
    B --> B2[Storage]
    B --> B3[Network]
    
    C --> C1[vRouter]
    C --> C2[vFirewall]
    C --> C3[vLoad Balancer]
    C --> C4[vWAN Accelerator]
    
    D --> D1[VNF Manager]
    D --> D2[NFV Orchestrator]
    D --> D3[Virtualized Infrastructure Manager]
```

**Benefits of NFV:**
- Reduced hardware costs
- Faster service deployment
- Scalability and flexibility
- Reduced power consumption
- Vendor independence

## 8. SD-WAN (Software-Defined Wide Area Network)

SD-WAN is a software-defined approach to managing wide-area networks, simplifying branch office connectivity and providing centralized control.

```mermaid
graph TD
    A[SD-WAN Architecture] --> B[SD-WAN Edge]
    A --> C[SD-WAN Controller]
    A --> D[SD-WAN Orchestrator]
    
    B --> B1[Branch Offices]
    B --> B2[Data Centers]
    B --> B3[Cloud Resources]
    
    C --> C1[Path Selection]
    C --> C2[Policy Management]
    C --> C3[Security Services]
    
    D --> D1[Zero-touch Provisioning]
    D --> D2[Monitoring]
    D --> D3[Analytics]
    
    B1 --- E[Transport Options]
    B2 --- E
    B3 --- E
    
    E --- E1[MPLS]
    E --- E2[Broadband]
    E --- E3[LTE/5G]
    E --- E4[Satellite]
```

**Key Capabilities:**
- Application-aware routing
- Dynamic path selection
- Transport independence
- Centralized policy management
- Integrated security
- Zero-touch provisioning
- Real-time analytics

**Benefits:**
- Reduced WAN costs
- Improved application performance
- Simplified operations
- Enhanced security
- Business agility
- Cloud connectivity

## Additional Resources

- [NIST Definition of Cloud Computing](https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-145.pdf)
- [AWS Cloud Computing](https://aws.amazon.com/what-is-cloud-computing/)
- [Microsoft Azure Cloud Computing](https://azure.microsoft.com/en-us/overview/what-is-cloud-computing/)
- [Google Cloud](https://cloud.google.com/learn/what-is-cloud-computing)
- [Open Networking Foundation](https://opennetworking.org/)
- [OpenDaylight Project](https://www.opendaylight.org/)
- [ETSI NFV](https://www.etsi.org/technologies/nfv)

## Practice Questions

1. Compare and contrast IaaS, PaaS, and SaaS, providing examples of each. For a startup developing a new web application, which service model would you recommend and why?

2. Explain the differences between public, private, and hybrid cloud deployment models. What factors would an organization consider when choosing between these models?

3. Describe the key components of a Virtual Private Cloud (VPC) and how they work together to provide network isolation and security in a public cloud environment.

4. How does Software-Defined Networking (SDN) differ from traditional networking? Explain the three layers of the SDN architecture and their interactions.

5. Describe how Network Function Virtualization (NFV) and SD-WAN are transforming enterprise networking. What benefits do these technologies provide compared to traditional approaches?
