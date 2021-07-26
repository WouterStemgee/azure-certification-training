# AZ-304: Microsoft Azure Architect Design
## Design Monitoring (10-15%)
### Design for cost optimization
- recommend a solution for cost management and cost reporting
- recommend solutions to minimize costs

### Design a solution for logging and monitoring
- determine levels and storage locations for logs
- plan for integration with monitoring tools including Azure Monitor and Azure Sentinel
- recommend appropriate monitoring tool(s) for a solution
- choose a mechanism for event routing and escalation
- recommend a logging solution for compliance requirements

## Design Identity and Security (25-30%)
### Design authentication
- recommend a solution for single-sign on
- recommend a solution for authentication
- recommend a solution for Conditional Access, including multi-factor authentication
- recommend a solution for network access authentication
- recommend a solution for a hybrid identity including Azure AD Connect and Azure AD

### Connect Health
- recommend a solution for user self-service
- recommend and implement a solution for B2B integration

### Design authorization
- choose an authorization approach
- recommend a hierarchical structure that includes management groups, subscriptions and
resource groups
- recommend an access management solution including RBAC policies, access reviews,
role assignments, Privileged Identity Management (PIM), Azure AD Identity Protection,
Just In Time (JIT) access

### Design governance
- recommend a strategy for tagging
- recommend a solution for using Azure Policy
- recommend a solution for using Azure Blueprints
- recommend a solution that leverages Azure Resource Graph

### Design security for applications
- recommend a solution that includes Key Vault
- recommend a solution that includes Managed Identities
- recommend a solution for integrating applications into Azure AD

## Design Data Storage (15-20%)
### Design a solution for databases
- select an appropriate data platform based on requirements
- recommend database service tier sizing
- recommend a solution for database scalability
- recommend a solution for encrypting data at rest, data in transmission, and data in use

### Design data integration
- recommend a data flow to meet business requirements
- recommend a solution for data integration, including Azure Data Factory, Azure

### Databricks, Azure Data Lake, Azure Synapse Analytics
Select an appropriate storage account
- choose between storage tiers
- recommend a storage access solution
- recommend storage management tools

## Design Business Continuity (10-15%)
### Design a solution for backup and recovery
- recommend a recovery solution for Azure hybrid and on-premises workloads that meets
recovery objectives (RTO, RLO, RPO)
- design and Azure Site Recovery solution
- recommend a solution for recovery in different regions
- recommend a solution for geo-redundancy of workloads
- recommend a solution for Azure Backup management
- design a solution for data archiving and retention

### Design for high availability
- recommend a solution for application and workload redundancy, including compute,
database, and storage
- recommend a solution for autoscaling
- identify resources that require high availability
- identify storage types for high availability

## Design Infrastructure (25-30%)
### Design a compute solution
- recommend a solution for compute provisioning
- determine appropriate compute technologies, including virtual machines, App Services,
Service Fabric, Azure Functions, Windows Virtual Desktop, Batch, HPC and containers
- recommend a solution for containers
- recommend a solution for automating compute management

### Design a network solution
- recommend a network architecture (hub and spoke, Virtual WAN)
- recommend a solution for network addressing and name resolution
- recommend a solution for network provisioning
- recommend a solution for network security including Private Link, firewalls, gateways,
network segmentation (perimeter networks/DMZs/NVAs)
- recommend a solution for network connectivity to the Internet, on-premises networks,
and other Azure virtual networks
- recommend a solution for automating network management
- recommend a solution for load balancing and traffic routing

### Design an application architecture
- recommend a microservices architecture including Event Grid, Event Hubs, Service Bus,
Azure Queue Storage, Logic Apps, Azure Functions, Service Fabric, AKS, Azure App

### Configuration and webhooks
- recommend an orchestration solution for deployment and maintenance of applications
including ARM templates, Azure Automation, Azure Pipelines, Logic Apps, or Azure
Functions
- recommend a solution for API integration

### Design migrations
- assess and interpret on-premises servers, data, and applications for migration
- recommend a solution for migrating applications and VMs
- recommend a solution for migration of databases
- determine migration scope, including redundant, related, trivial, and outdated data
- recommend a solution for migrating data (Storage Migration Service, Azure Data Box,
Azure File Sync-based migration to hybrid file server)