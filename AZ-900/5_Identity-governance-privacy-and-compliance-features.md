# 5. Identity, governance, privacy, and compliance features (20-25%)
## 5.1 Azure identity services
### Authentication vs. authorization
- Authentication: process of verifying the identity of a person/service that wants to access a resource
- Authorization: establishing what level of access an authenticated person/service has

### Azure Active Directory
- Active Directory
    - identity and access management service managed by your own organization
- Azure AD vs AD
    - AD: on-premises environments
    - Azure AD: cloud-based (globally available)
- Users
    - IT administrators: control access to applications/resources based on their business requirements
    - App developers: can use Azure AD to provide standards-based approach for adding functionality to applications (SSO, enabling app to work with user's existing credentials)
    - Users: manage their own identities (self-service password reset)
    - Online service subscribers: Microsoft (Office) 365, Microsoft Dynamics CRM Online (all are tenants)
        - "tenant": representation of an organization, typically separated from other tenants, has their own identity
- Services
    - Authentication
    - Single sign-on
    - Application management
    - Device management
- Resources
    - internal resources: apps on corporate network/intranet
    - external resources: Office 365, Azure portal, other (SaaS) apps
- Connectivity: Azure AD Connect
    - synchronizes user identities between on-premises AD and Azure AD, synchronizes changes between both identity systems
        SSO, MFA, self-service password reset: available under both systems

### Conditional Access, Multi-Factor Authentication (MFA), Single Sign-On (SSO)
- Conditional Access
    - tool that Azure Active Directory uses to allow/deny access to resources based on **identity signals**
        - signals include who the user is, where the user is, and what device the user is requesting access from
    - more granular MFA experience for users
        - example: no MFA challenge when the second authentication comes from a known location/device
    - use cases:
        - MFA required to access an application
        - make services only accessible through approved client applications
        - require users to access your application only from managed devices
        - block access from untrusted sources, such as access from unknown or unexpected locations
    - requires Azure AD Premium P1 or P2 license
- Multi-Factor Authentication (MFA)
    - process where user is prompted during the sign-in process for an additional form of identification
        - 2+ elements:
            - something the user **knows**: email address/password
            - something the user **has**: code sent to user's mobile phone
            - something the user **is**: biometric property
    - Azure AD Multi-Factor Authentication
        - enables users to choose an additional form of authentication during sign-in, such as a phone call or mobile app notification
        - provided in Azure Active Directory and Office 365
- Single Sign-On (SSO)
    - enables a user to sign in one time and use that credential to access multiple resources/applications from different providers
## 5.2 Governance, Privacy and compliance features
###  Cloud Adoption Framework for Azure
- Cloud Adoption Framework
    - provides guidance to help with your cloud adoption journey
    - stages:
        1. Define your strategy
            - define and document your motivations: meeting with stakeholders and leadership can help you answer why you're moving to the cloud
            - document business outcomes: meet with leadership from your finance, marketing, sales, and human resource groups to help you document your goals
            - develop a business case: validate that moving to the cloud gives you the right return on investment (ROI) for your efforts
            - choose the right first project: choose a project that's achievable but also shows progress toward your cloud migration goals
        2. Make a plan
            - digital estate: create an inventory of the existing digital assets and workloads that you plan to migrate to the cloud
            - initial organizational alignment: ensure that the right people are involved in your migration efforts, both from a technical standpoint as well as from a cloud governance standpoint
            - skills readiness plan: build a plan that helps individuals build the skills they need to operate in the cloud
            - cloud adoption plan: build a comprehensive plan that brings together the development, operations, and business teams toward a shared cloud adoption goal
        3. Ready your organization
            - Azure setup guide: review the Azure setup guide to become familiar with the tools and approaches you need to use to create a landing zone
            - Azure landing zone: begin to build out the Azure subscriptions that support each of the major areas of your business, a landing zone includes cloud infrastructure as well as governance, accounting, and security capabilities
            - expand the landing zone: refine your landing zone to ensure that it meets your operations, governance, and security needs
            - best practices: start with recommended and proven practices to help ensure that your cloud migration efforts are scalable and maintainable
        4. Adopt the cloud
            - migrate your first workload: use the Azure migration guide to deploy your first project to the cloud
            - migration scenarios: use additional in-depth guides to explore more complex migration scenarios
            - best practices: check in with the Azure cloud migration best practices checklist to verify that you're following recommended practices
            - process improvements: identify ways to make the migration process scale while requiring less effort
            - innovate:
                - business value consensus: verify that investments in new innovations add value to the business and meet customer needs
                - Azure innovation guide: use this guide to accelerate development and build a minimum viable product (MVP) for your idea
                - best practices: verify that your progress maps to recommended practices before you move forward
                - feedback loops: check in frequently with your customers to verify that you're building what they need
        5. Govern and manage your cloud environments
            - methodology: consider your end state solution. Then define a methodology that incrementally takes you from your first steps all the way to full cloud governance
            - benchmark: use the governance benchmark tool to assess your current state and future state to establish a vision for applying the framework
            - initial governance foundation: create an MVP that captures the first steps of your governance plan
            - improve the initial governance foundation: iteratively add governance controls that address tangible risks as you progress toward your end state solution
            - manage
                - establish a management baseline: Define your minimum commitment to operations management. A management baseline is the minimum set of tools and processes that should be applied to every asset in an environment.
                - define business commitments: document supported workloads to establish operational commitments with the business and agree on cloud management investments for each workload
                - expand the management baseline: apply recommended best practices to iterate on your initial management baseline
                - advanced operations and design principles: for workloads that require a higher level of business commitment, perform a deeper architecture review to deliver on your resiliency and reliability commitments

### Subscription governance strategy
- Billing
    - create one billing report per subscription, if you have multiple departments and need to do a "chargeback" of cloud costs, one possible solution is to organize subscriptions by department or by project
    - resource tags: define how many subscriptions you need and what to name them, take into account your internal billing requirements
- Access control
    - every subscription is associated with an Azure Active Directory tenant, each tenant provides administrators the ability to set granular access through defined roles by using **Azure role-based access control**
- Subscription limits
    - subscriptions also have resource limitations
        - example: maximum number of network Azure ExpressRoute circuits per subscription is 10
    - should be considered your design phase
    - management groups: manages access, policies, and compliance across multiple Azure subscriptions
### Azure role-based access control (RBAC)
- RBAC: control access to resources in the Azure cloud environment by defining a **scope**
    - scope can include:
        - Management group (a collection of multiple subscriptions)
        - Single subscription
        - Resource group
        - Single resource
    - roles
        - **Owner** user in management group scope: manage everything in all subscriptions within the management group
        - **Reader** in subscription scope: view every resource group/resource within subscription
        - **Contributor** in resource group scope: manage resources of all types within that resource group, but not other resource groups within the subscription
- "Allow model"
    - assigned roles allows you to perform certain actions (read/write/delete)
- Managing Azure RBAC permissions
    - Access control (IAM) pane in Azure portal

### Resource Locks
- **Resource lock**: prevents resources from being accidentally deleted or changed
    - **CanNotDelete** 
    - **ReadOnly** 

### Resource Tagging
- Extra **metadata** for organizing resources
    - Resource management
    - Cost management and optimization
    - Operations management
    - Security
    - Governance and regulatory compliance
    - Workload optimization and automation
- Example: tagging structure
    - AppName: name of the application that the resource is part o
    - CostCenter: internal cost center code
    - Owner: name of the business owner who's responsible for the resource
    - Environment: environment name, such as "Prod," "Dev," or "Test"
    - Impact: important the resource is to business operations, such as "Mission-critical", "High-impact", or "Low-impact"

### Azure Policy
- **Azure Policy**: enables you to create, assign, and manage policies that control or audit your resources
    - define both individual policies and groups of related policies (**initiatives**)
    - comes with a number of built-in policy and initiative definitions
        - example: policy that allows only a certain stock-keeping unit (SKU) size of virtual machines (VMs) to be used in your environment
    - Azure Policy can automatically remediate noncompliant resources and configurations to ensure the integrity of the state of the resources
        - example: if all resources in a certain resource group should be tagged with the "AppName" tag and a value of "SpecialOrders", Azure Policy can automatically reapply that tag if it has been removed
    - integrates with Azure DevOps by applying any **continuous integration and delivery pipeline policies** that apply to the pre-deployment and post-deployment phases of your applications
- Usage:
    1. Create a policy definition
        - examples:
            - Allowed virtual machine SKUs
            - Allowed locations
            - MFA should be enabled on accounts with write permissions on your subscription
            - CORS should not allow every resource to access your web applications
            - System updates should be installed on your machines
    2. Assign the definition to resources
    3. Review the evaluation results.
- **Azure Policy initiatives**: grouping related policies into one set
    - example initiative: monitor all of the available security recommendations for all Azure resource types in Azure Security Center
        - Under this initiative, the following policy definitions are included
            - Monitor unencrypted SQL Database in Security Center
            - Monitor OS vulnerabilities in Security Center
            - Monitor missing Endpoint Protection in Security Center

### Azure Blueprints
- **Azure Blueprints**: define a repeatable set of governance tools and standard Azure resources that your organization requires
    - usable across multiple subscriptions
    - orchestrates the deployment of various resource templates and other artifacts, such as:
        - Role assignments
        - Policy assignments
        - Azure Resource Manager templates
        - Resource groups
    - usage: 
        1. Create an Azure blueprint
        2. Assign the blueprint
        3. Track the blueprint assignments
    - **blueprint artifacts**: each component in the blueprint definition is known as an artifact

## Microsoft core tenets of Security, Privacy and Compliance
- Compliance categories available on Azure

![](img/compliance-matrix.png)

### Microsoft Privacy Statement, Product Term site, Data Protection Addendum (DPA)
- **Data Protection Addendum** (DPA): defines the data processing and security terms for online services
    - Compliance with laws
    - Disclosure of processed data
    - Data Security, which includes security practices and policies, data encryption, data access, customer responsibilities, and compliance with auditing
    - Data transfer, retention, and deletion
- **Microsoft Privacy Statement**: explains what personal data Microsoft collects, how Microsoft uses it, and for what purposes
- **Online Services Terms**: legal agreement between Microsoft and the customer

[Licensing Terms and Documentation Search](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx)
### Trust Center
- **Trust Center**: showcases Microsoft's principles for maintaining data integrity in the cloud and how Microsoft implements and supports security, privacy, compliance, and transparency in all Microsoft cloud products and services
    - In-depth information about security, privacy, compliance offerings, policies, features, and practices across Microsoft cloud products
    - Additional resources for each topic
    - Links to the security, privacy, and compliance blogs and upcoming events

[Trust Center](https://www.microsoft.com/nl-be/trust-center)
### Azure compliance documentation
- access detailed documentation about legal and regulatory standards and compliance on Azure
- compliance offerings categories:
    - Global
    - US government
    - Financial services
    - Health
    - Media and manufacturing
    - Regional

[Azure compliance documentation](https://docs.microsoft.com/en-us/azure/compliance/)
### Azure Sovereign Regions (Azure Government cloud services and Azure China cloud services)
- **Azure Government**: separate instance of the Microsoft Azure service
    - addresses the security and compliance needs of US federal agencies, state and local governments, and their solution providers
    - offers physical isolation from non-US government deployments and provides screened US personnel
- **Azure China 21Vianet**: physically separated instance of cloud services located in China
    -  independently operated and transacted by Shanghai Blue Cloud Technology Co., Ltd. ("21Vianet")