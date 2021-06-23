# 3. Core solutions and management tools on Azure (10-15%)
## 3.1 Core solutions available in Azure
### IoT Hub, IoT Central, Azure Sphere
- **IoT Hub**: bare IoT messaging services
- **IoT Central**: dashboard/UI build on top of IoT Hub
- **Azure Sphere**: focussed on adding end-to-end security on top of IoT Central

### Azure Synapse Analytics, HDInsight, Azure Databricks

### Azure Machine Learning, Cognitive Services, Azure Bot Service
- **Azure Machine Learning**: flexible experimentation tools/services to train/test/deploy models to predict future outcomes using your own datasets
- Azure Cognitive Services: prebuilt general purpose machine learning models for NLP (Language, Speech, Vision, Decision)
    - Personalizer service: watch users' actions within applications for personalized recommendations
- **Azure Bot Service** and Bot Framework: manage virtual chatbot agents built using Azure Cognitive Services

### Azure Functions, Logic Apps
- **Azure Functions**: event-driven serverless platform
    - Events: HTTP request, new message on queue, timer, ...
    - Supports multiple programming languages (C#, Python, JavaScript, Typescript, Java, PowerShell)
    - Scales automatically based on demand
    - Stateless environment
        - if state is required: connect function to Azure storage account using bindings
    - Durable Functions: used for orchestration tasks (chain together functions while maintaining state between them)
- **Azure Logic Apps**: Low/no-code development platform used for automation/orchestration of workflows/business processes
    - Simplifies integrations for apps, data, systems, enterprise applications (EAI) and business-to-business (B2B)
    - Web-based designer: build app by linking triggers to actions with connectors
        - Trigger = event
        - Action = task/step to execute
    - Gallery of 200+ connectors available for integrating with all kind of existing services

### Azure DevOps, GitHub Actions, Azure DevTest Labs
- **Azure DevOps services**: suite of services (SaaS) that address every stage of the software development lifecycle
    - Azure Repos: centralized source-code repository
    - Azure Boards: Kanban boards used for project management
    - Azure Pipelines: CI/CD pipeline automation tool
    - Azure Artifacts: repository for hosting artifacts (compiled source code, packages, ...) which can be fed into testing or deployment pipeline steps
    - Azure Test Plans: automated test tool that can be used in CI/CD pipelines
- **GitHub and GitHub Actions**: decentralized source-code management tool build on top of Git, GitHub Actions enables workflow automation with triggers for many lifecycle events mainly used for automating CI/CD toolchains
    - Azure DevOps vs. GitHub: GitHub more focussed on open-source projects, Azure DevOps more focussed on enterprise development with heavier project-management and planning tools + more granular control of permissions
- **Azure DevTest Labs**: automation/management of building/configuring/deploying/teardown of software projects in VMs in development/testing environments


## 3.2 Azure management tools
- Management tools
    - visual tools: user friendly
    - code-based tools: used for large deployments of resources with interdependencies and configuration options
- Infrastructure-as-code
    - imperative code: describes each individual step to achieve desired outcome
    - declarative code: describes desired outcome

### Resource Management: Azure Portal, Azure PowerShell, Azure CLI, Cloud Shell, Azure Mobile App, Azure Resource Manager (ARM) templates
- **Azure Portal**: web-based user interface 
    - manage services, view reports
- **Azure PowerShell**: execute _PowerShell cmdlets_
    - calls Azure Rest API to perform management tasks
    - cmdlets can be combined into a script
    - can be run through Azure Cloud Shell
    - useful for one-off management and administrative tasks
- **Azure CLI**: executable program that can execute _Bash commands_ to interact with the Azure Rest API
    - useful if you come from a Linux background
- **Cloud Shell**: used to run PowerShell cmdlets on Azure
- **Azure Mobile App**: iOS/Android application
    - monitor health status of Azure resources, check alerts, diagnose issues, restart apps/VMs
    - run Azure CLI/PowerShell commands
- **ARM templates**: describe resources you want to use in a declarative JSON format
    - benefit: entire ARM template is verified before any code is executed to ensure that resources will be created and connected correctly, resource creation is orchestrated in parallel (all are created at the same time)
    - desired state and configuration of each resource is defined in the ARM template
    - can execute Bash/PowerShell scripts before/after resource setup
    - used for repeatable deployments

### Monitoring: Azure Advisor, Azure Monitor, Azure Service Health
- **Azure Advisor**: evaluates Azure resources and makes recommendations to help make improvements in reliability, security, performance, operational excellence and costs
    - available via Azure portal and API
    - ability to setup notifications to alert for new recommendations
- **Azure Monitor**: platform for collecting, analyzing, visualizing metric and logging data collected at every layer in the application architecture (Application, OS, Resources, Subscription, Tenant, ...)
    - Insights: application/container/VM/monitoring solutions
    - Visualize: dashboards, views, Power BI, workbooks
    - Analyze: metric analytics, log analytics
    - Respond: alerts, autoscale
    - Integrate: Logic Apps, export APIs
- **Azure Service Health**: personalized view of the health of Azure services, regions and resources
    - [status.azure.com](http://status.azure.com) website
    - service issues, planned maintenance, health advisories, incident reports (root cause analyses/RCAs)
