# 4. General security and network security features (10-15%)
## 4.1 Azure security features
### Azure Security Center
- Monitoring service that provides visibility of "security posture" across all services (both on Azure + on-premises)
    - **security posture**: refers to cybersecurity policies and controls to predict/prevent/respond security threats
    - automatically applies required security settings to new resources
    - provides security recommendations based on current config
    - uses machine learning to detect/block malware
        - alternative: adaptive application controls: define application rules in whitelist/blacklist
    - detect/analyze potential inbound attacks, investigate threats/post-breach activities
    - just-in-time access control for network ports: reduces attack surface, only required traffic allowed at the time you need it to
- Security Posture
    - **policy & compliance report**: shows overall regulatory compliance from a security perspective and indicates what resources that need to remediate
    - **security alerts**: centralized view of all security alerts
        - dismiss false alerts, manually investigate
        - set automated response with workflow automation
    - **secure score**: measurement of an organization's security posture based on security controls that are satisfied
    - **resource security hygiene**: see the health of all resources to help prioritize remediation actions (low, medium, high severity)
- Defense capabilities for VMs, network security, file integrity
    - **just-in-time VM access**: block traffic by default to specific network ports/VMs, only allow traffic for a specified time when an admin requests and approves it
    - **adaptive application controls**: control which applications are allowed to run on its VMs, creates exception rules for each resource group that holds the VMs and provides recommendations
        - provides alerts to inform company about unauthorized applications that are running on its VMs
    - **adaptive network hardening**: monitor internet traffic patterns for VMs and compare those patterns with the company's network security group (NSG) settings
    - **file integrity monitoring**: monitor changes to important files on Windows/Linux, registry settings, applications, ...

### Azure Sentinel
- Security Information and Event Management (SIEM) system
    - aggregates security data from many different sources
    - provides capabilities for threat detection and response (Built in analytic templates)
- Capabilities
    - collect cloud data at scale
    - detect previously undetected threats
    - investigate threats with AI
    - respond to incidents rapidly
- Data Sources
    - Microsoft solutions: Microsoft (Office) 365, Azure AD, Windows Defender Firewall
    - other services/solutions: AWS CloudTrail, Citrix analytics, VMWare Carbon Black Cloud, ...
    - industry-standard data sources: data that uses the Common Event Format (CEF) messaging standard, Syslog, or REST API
- Azure Monitor Workbooks: automate responses to threats

### Key Vault
- Centralized cloud service for storing application secrets in a single central location
    - provides access to sensitive information by providing access control and logging capabilities
- Capabilities
    - manage secrets
    - manage encryption keys
    - SSL/TLS certificates
    - store secrets backed by hardware security modules (HSMs)
- Benefits
    - centralized application secrets
    - securely stored secrets and keys
    - access monitoring and access control of application secrets
    - simplified administration of application secrets
    - integration with other Azure services

### Azure Dedicated Hosts
- Dedicated physical servers to host your Azure VMs for Windows/Linux
    - some organizations must follow regulatory compliance that required them to be the only customer using the physical machine that hosts their VMs
    - regular Azure VMs run on shared hardware that Microsoft manages
- Benefits
    - gives visibility/control over server infrastructure
    - helps address compliance requirements (isolated server)
    - able to choose number of CPUs, server capabilities, VM series, VM sizes
- Availability considerations
    - for HA: provision multiple hosts in a "host group", and deploy VMs across this group
    - maintenance control: features that enables control during maintenance updates within 35-day rolling window
- Pricing
    - charged per dedicated host, independent of number of VMs you deploy on it
    - price based on VM family, type (hardware size), region
    - software licensing, storage/network usage are billed separately

## 4.2 Azure network security
### Network Security Groups (NSG)
### Azure Firewall
### Azure DDoS protection
### Concept of defense
