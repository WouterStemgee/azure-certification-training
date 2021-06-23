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
- Azure Portal, Azure PowerShell, Azure CLI, Cloud Shell, Azure Mobile App
- Azure Advisor
- Azure Resource Manager (ARM) templates
- Azure Monitor
- Azure Service Health