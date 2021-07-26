# Notes
## M1. Design Azure compute services
![](img/choose-compute-service.png)
- https://docs.microsoft.com/en-us/azure/cloud-adoption-framework/ready/enterprise-scale/architecture
- managed services less expensive than unmanaged services
- IaaS vs PaaS: shared responsibility
    - https://docs.microsoft.com/en-us/azure/security/fundamentals/shared-responsibility
- Azure well-architected framework pillars
    - cost optimization
    - operational excellence
    - permorance efficiency
    - reliability
    - security
- To avoid hard limits in subscriptions, you can create multiple subscriptions
- Service level agreements: listen to the business requirements and see what SLA is necessary
    - https://docs.microsoft.com/en-us/azure/architecture/framework/resiliency/business-metrics#understand-service-level-agreements
- https://azurecharts.com/
- Azure Resource Explorer
    - browse all resources, see ARM JSON files

## M2. Design Azure Networking
- communication between VNETs (different locations/tenants/subscriptions)
    1. **peering**
        - fast deployment
        - not expensive
        - private
    2. VNET-TO-VNET
        - encrypted (IPsec VPN)
        - slow deployment
        - expensive
- protect traffic between 2 subnets of 2 VNETs
    - **Network Security groups** (NSG): 
        - firewall that you can attach to a NIC (public/private IP) or a subnet
            - VM: control traffic in/out Linux (iptables) and Windows (Windows Firewall) machines
                - OS level firewall
            - subnet: control traffic between VMs on the subnet
        - https://docs.microsoft.com/en-us/azure/virtual-network/virtual-networks-faq#what-are-the-constraints-related-to-global-vnet-peering-and-load-balancers
- planning for virtual networks
    - criteria
        - latency (based on geolocation)
        - availability 
        - price
        - laws (GDPR)
    - address space, subnets, regions, subscription
        - VNET is scoped to a single region/location (use VNET peering)
    - UDR: User-defined route, managed by Azure
    - Azure Policy
        - apply policy on subscriptions, all users that use subscription are impacted
    - Azure DNS
        - set custom DNS rules
        - https://docs.microsoft.com/en-us/azure/active-directory-domain-services/manage-dns
    - Azure Load Balancer vs. Azure Application Gateway
        - Azure Load Balancer: L2 & L3 -> uses NSGs
            - used internally attched to NICs or subnets
        - Azure Application Gateway (HTTP): L7 -> uses WAF (Web Application Gateway)
            - sits in between public internet and private VMs, this way VMs are not exposed directly
- LoadBalancer, 4 services: https://docs.microsoft.com/en-us/azure/architecture/guide/technology-choices/load-balancing-overview
    1. DNS resolution: Azure Traffic Manager. 
    2. Azure Load Balancer (layer 3). 
    3. Azure FrontDoor (same than Application Gateway but global reach). 
    4. Application Gateway (layer 7).
    ![](img/load-balancing-decision-tree.png)
- Network integration
    - Azure ExpressRoute: https://azure.microsoft.com/en-us/pricing/details/expressroute/
- Bastion
    - ![](img/bastion-networking.png)