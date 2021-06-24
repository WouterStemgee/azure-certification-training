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
### Defense in depth
- Layers + Defense tools/features:
    1. **Physical Security**: hardware in datacenter
        - physical safeguards in datacenter
    2. **Identity & Access**: infrastructure access & change control
        - single sign-on (SSO) and MFA
        - audit events + changes
    3. **Perimeter**: DDoS protection to filter large-scale attacks
        - perimeter firewalls to identify/alert on malicious attacks
    4. **Network**: limit communications between resources through segmentation and access controls
        - deny by default
        - restrict inbound internet access, limit outbound access
        - implement secure connectivity to on-premises networks
    5. **Compute**: access to VMs
        - secure access to VMs
        - implement endpoint protection on devices
        - keep systems patched and current
    6. **Application**: application security vulnerabilities
        - store sensitive application secrets in secure storage medium
        - make security a design requirement
    7. **Data**: business/customer data that needs protection (database data, VM disk data, SaaS data, cloud storage data)
        - data administrators are responsible for ensuring it's properly secured
        - often regulatory requirements ensure confidentiality, integrity and availability of data (**security posture**)
            - **confidentiality**: principle of least privilege: restricting access to information only to individuals explicitly granted access
            - **integrity**: prevent unauthorized changes to information (at rest + in transit) using unique fingerprint of the data (hash)
            - **availability**: ensure services are functioning and can be accessed only by authorized users

### Azure Firewall
- Azure Firewall: managed, cloud-based network security service that helps protect resources in Azure virtual networks
    - **stateful firewall**: analyzes the complete context of a network connection (not just individual packets)
    - implements high availability and unrestricted cloud scalability
    - central location to create/enforce/log application/network connectivity policies across subscriptions/virtual networks
    - inbound/outbound filtering rules
    - inbound Destination Network Address Translation (DNAT) support
    - Azure Monitor logging
- Configuration options
    - application rules that define FQDNs that can be accessed from a subnet
    - network rules that define source address, protocol, destination port/address
    - network address translation (NAT) rules that define destination IP addresses/ports to translate inbound requests
- Azure Application Gateway, Azure Front Door, Azure Content Delivery Network: possesses internal web application firewall (**WAF**)
    - provides centralized, inbound protection for your web applications against common exploits/vulnerabilities

### Azure DDoS protection
- DDoS attacks: distributed denial of service attacks
    - attempts to overwhelm and exhaust an application's resources, making the application slow/unresponsive to legitimate users
    - can target any publicly reachable resource through the internet
- Azure DDoS protection: helps protect Azure resources from DDoS attacks
    - recommends application design practices
    - analyzes/discards DDoS traffic at the Azure network edge
    - global Azure network is used to distribute and mitigate attack traffic across Azure regions
- Service Tier plans: 
    - **Basic**: automatically enabled for free as part of an Azure subscription
        - always-on network traffic monitoring
        - real-time mitigation of common network-level attacks
        - ensures Azure infrastructure itself is not affected
    - **Standard**: provides additional mitigation capabilities, tuned specifically to Azure Virtual Network resources
        - dedicated traffic monitoring is used to tune protection policies
            - policies are applied to public IP addresses associated with Azure Load Balancers or Application Gateways
        - uses machine learning algorithms
- Attack types
    - Volumetric attacks: network flooding with substantial amount of seemingly legitimate traffic
    - Protocol attacks: exploits a weakness in the L3 & L4 protocol stacks
    - L7 application layer attacks: targets web application packets to disrupt the transmission of data between hosts
        - WAF offers protection against L7 attacks
        - standard tier plan protects the WAF itself from volumetric and protocol attacks

### Network Security Groups (NSG)
- Network Security Groups: filter network traffic to and from Azure resources within an Azure virtual network ("internal firewall")
    - contains multiple inbound/outbound **security rules** that enables to filter traffic to/from resouces by source/destination IP address/port/protocol
#### Exercise: Configuring NSG rule through Azure CLI
- Create Linux VM: `az vm create --resource-group <rg> --name <name> --image <image> --admin-user <admin-user> --generate-ssh-keys`
- Install nginx by running a Bash script using the "Custom Script Extension": 
    ```
    az vm extension set \
    --resource-group <rg> \
    --vm-name my-vm \
    --name customScript \
    --publisher Microsoft.Azure.Extensions \
    --version 2.1 \
    --settings '{"fileUris":["https://raw.githubusercontent.com/MicrosoftDocs/mslearn-welcome-to-azure/master/configure-nginx.sh"]}' \
    --protected-settings '{"commandToExecute": "./configure-nginx.sh"}'
    ```
- Access webserver
    - get VM IP address: `az vm list-ip-addresses`
    - store IP address in local variable:
        ```
        IPADDRESS="$(az vm list-ip-addresses \
        --resource-group <rg> \
        --name my-vm \
        --query "[].virtualMachine.network.publicIpAddresses[*].ipAddress" \
        --output tsv)"
        ```
    - create network security group rule: allow inbound access on port 80 (HTTP)
        - show list of NSG associated with the VM
            ```
            az network nsg list \
            --resource-group <rg> \
            --query '[].name' \
            --output tsv
            ```
        - show list of associated rules of the NSG associated with the VM
            ```
            az network nsg rule list \
            --resource-group <rg> \
            --nsg-name my-vmNSG \
            --query '[].{Name:name, Priority:priority, Port:destinationPortRange, Access:access}' \
            --output table
            ```
            ```
            Name               Priority    Port    Access
            -----------------  ----------  ------  --------
            default-allow-ssh  1000        22      Allow
            ```
        - create new NSG rule for inbound HTTP traffic on port 80
            ```
            az network nsg rule create \
            --resource-group <rg> \
            --nsg-name my-vmNSG \
            --name allow-http \
            --protocol tcp \
            --priority 100 \
            --destination-port-ranges 80 \
            --access Allow
            ```
            ```
            Name               Priority    Port    Access
            -----------------  ----------  ------  --------
            default-allow-ssh  1000        22      Allow
            allow-http         100         80      Allow
            ```
    - access website: `curl --connect-timeout 5 http://$IPADDRESS`
        - output:
            ```
            <html><body><h2>Welcome to Azure! My name is my-vm.</h2></body></html>
            ```