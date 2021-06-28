# 6. Azure Cost Management, SLA (10-15%)
## 6.1 Methods for planning and managing costs
### Factors that can affect costs (resource type, services, locations, ingress & egress traffic)
- Resource type
    - Usage meters: resource usage
- Services
    - Azure subscription types
    - Azure Marketplace
- Locations
- Zones for billing of network traffic
    - ingress & egress

### Factors that can reduce costs (reserved instances, reserved capacity, hybrid use benefit, spot pricing)
- Reserved instances
- Reserved capacity
- Hybrid use benefit
- Spot pricing

### Pricing calculator and Total Cost of Ownership (TCO) calculator
- **Pricing calculator**: estimate workload cost
    - [Pricing Calculator](https://azure.microsoft.com/nl-nl/pricing/calculator/)
- **TCO Calculator**: helps you estimate the cost savings of operating your solution on Azure over time, instead of in your on-premises datacenter
    - [TCO Calculator](https://azure.microsoft.com/nl-nl/pricing/tco/calculator/)
    - "total cost of ownership": includes all the hidden costs related to operating a technology capability on-premises, software licenses and hardware
    - Steps:
        1. Define your workloads: servers, databases, storage, networking
        2. Adjust assumptions
            - reusing on-premises licenses
            - specify whether you need to replicate storage to another region
            - key operating cost assumptions across several different areas vary among teams and organizations (electricity price, hourly pay rate IT support, network maintenance cost)
        3. View the report
### Azure Cost Management
- Azure subscriptions
    - Free trial
    - Pay-as-you-go
    - Member offers
- 3 ways to purchase services on Azure:
    - Through an Enterprise Agreement
    - Directly from the web
    - Through a Cloud Solution Provider
- Do's:
    - Understand *estimated costs* before you deploy
    - Use **Azure Advisor** to monitor your usage
    - Use **spending limits** to restrict your spending
    - Use **Azure Reservations** to prepay
    - Choose low-cost locations and regions
    - Research available cost-saving offers
    - Use Azure Cost Management + Billing to control spending
        - Reporting
        - Data enrichment
        - Budgets
        - Alerting
        - Recommendations
    - Apply **tags** to identify cost owners
    - Resize underutilized virtual machines
    - Deallocate virtual machines during off hours
    - Delete unused resources
    - Migrate from IaaS to PaaS services
    - Save on licensing costs
        - Choose cost-effective operating systems
        - Use Azure Hybrid Benefit to repurpose software licenses on Azure
## 6.2 Azure Service Level Agreements (SLAs) and service lifecycles
### Azure Service Level Agreement (SLA)
- Service-level agreement (SLA): formal agreement between a service company and the customer
    - defines the performance standards that Microsoft commits to for you, the customer
    - helps you understand what guarantees you can expect
    - the availability of the services that you use affect your application's performance
    - some SLAs focus on other factors as well, including latency, or how fast the service must respond to a request
- Sections
    - Introduction: explains what to expect in the SLA, including its scope and how subscription renewals can affect the terms
    - General terms: contains terms that are used throughout the SLA so that both parties have a consistent vocabulary
    - SLA details: defines the specific guarantees for the service
        - typically ranges from 99.9 percent ("three nines") to 99.99 percent ("four nines")
- Percentages vs. Total downtime:
    | SLA percentage 	| Downtime per week 	| Downtime per month 	| Downtime per year 	|
    |----------------	|-------------------	|--------------------	|-------------------	|
    | 99             	| 1.68 hours        	| 7.2 hours          	| 3.65 days         	|
    | 99.9           	| 10.1 minutes      	| 43.2 minutes       	| 8.76 hours        	|
    | 99.95          	| 5 minutes         	| 21.6 minutes       	| 4.38 hours        	|
    | 99.99          	| 1.01 minutes      	| 4.32 minutes       	| 52.56 minutes     	|
    | 99.999         	| 6 seconds         	| 25.9 seconds       	| 5.26 minutes      	|
    -  amounts are cumulative: duration of multiple different service outages would be combined, or added together
- **Service credit**: the percentage of the fees you paid that are credited back to you according to the claim approval process
    - you might receive a discount on your Azure bill as compensation when a service fails to perform according to its SLA

[Service Level Agreements](https://azure.microsoft.com/nl-nl/support/legal/sla/)
### Service lifecycle in Azure
- **Service lifecycle**: defines how every Azure service is released for public use
    - Development phase: Azure team collects and defines its requirements, and begins to build the service
    - **Public preview** phase: the public can access and experiment with it so that it can provide feedback
    - **General availability** (GA): after a new Azure service is validated and tested, it's released to all customers as a production-ready service