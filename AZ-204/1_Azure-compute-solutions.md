# 1. Develop Azure compute solutions (25-30%)
## 1.1 Implement IaaS solutions
### provision virtual machines (VMs)
- create VM
    1. navigate Azure Portal -> Create a Resource (+) -> Compute
        - pick OS image
    2. "Create a virtual machine" wizard
        - Subscription
        - Resource group
            - alternative script: create rg
                ```ps
                New-AzResourceGroup -Name "myResourceGroup" -Location "EastUS"
                ```
        - VM name, Region, Image
        - Size (CPUs, RAM, Disks)
        - Administrator account (username, password)
        - Public inbound ports: allow selected ports (HTTP, HTTPS, SSH, RDP)
        - "Review & Create" > "Create"
            - alternative script: create VM
                ```ps
                $cred = Get-Credential 

                New-AzVM -Name MyVm -Credential $cred -ResourceGroupName MyResourceGroup -Image win2016datacenter -Size Standard_D2S_V3
                ```
- encrypt *.VHD disk using BitLocker ([docs](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/disk-encryption-powershell-quickstart))
    1. create Azure KeyVault configured for encryption keys in same region of VM
        - script: 
            ```ps
            New-AzKeyvault -name MyKV -ResourceGroupName myResourceGroup -Location EastUS -EnabledForDiskEncryption
            ```
    2. encrypt in Azure Cloud Shell: `Set-AzVMDiskEncryptionExtension`
        - script: 
            ```ps
            $KeyVault = Get-AzKeyVault -VaultName MyKV -ResourceGroupName MyResourceGroup

            Set-AzVMDiskEncryptionExtension -ResourceGroupName MyResourceGroup -VMName MyVM -DiskEncryptionKeyVaultUrl $KeyVault.VaultUri -DiskEncryptionKeyVaultId $KeyVault.ResourceId
            ```
### configure, validate, and deploy ARM templates
- configure ARM template
    1. "Create a virtual machine" wizard 
    2. "Download a template for automation"
        - Template screen: 
            - template (JSON file): 
                - parameters: virtualMachineName, osDiskType, adminUsername, adminPassword, ...       
                    - usage: `"[parameters('virtualMachineName')]"`
                - variables
                - resources
        - Parameters screen: 
            - parameter definitions (JSON file)
                ```
                "parameters": {
                    "virtualMachineName": {
                        "value": "myVM"
                    }
                }
                ```
        - PowerShell screen:
            - script to execute template + parameters files
    3. "Download"
        - modify on local machine
    4. "Add to library"
        - stored in Azure

### configure container images for solutions
- docker: [docs](https://docs.docker.com/engine/reference/builder/)
    - Dockerfile
- docker-compose

### publish an image to the Azure Container Registry
1. create ACR
    - navigate Azure Portal -> Create a Resource (+) -> Containers
        - pick Container registry
2. login to ACR using Azure CLI: `az acr login`
3. Dockerfile -> build -> tag -> push image to Azure Container Registry
4. check image in repository: Azure Portal -> Container registry -> Repositories

### run containers by using Azure Container Instance
1. create ACI
    - navigate Azure Portal -> Azure Cloud Shell: Bash
        - Create rg: `az group create --name learn-deploy-aci-rg --location eastus`
    - example: create container with environment variables (db connection credentials ) and mounted volume (Azure file share)
        ```bash
        az container create \
            --resource-group learn-deploy-aci-rg \
            --name mycontainer \
            --image microsoft/aci-helloworld \
            --ports 80 \
            --dns-name-label $DNS_NAME_LABEL \
            --location eastus
            --environment-variables \
                COSMOS_DB_ENDPOINT=$COSMOS_DB_ENDPOINT \
                COSMOS_DB_MASTERKEY=$COSMOS_DB_MASTERKEY
            --azure-file-volume-account-name $STORAGE_ACCOUNT_NAME \
            --azure-file-volume-account-key $STORAGE_KEY \
            --azure-file-volume-share-name aci-share-demo \
            --azure-file-volume-mount-path /aci/logs/
        ```
2. Check status
    ```bash
    az container show \
        --resource-group learn-deploy-aci-rg \
        --name mycontainer \
        --query "{FQDN:ipAddress.fqdn,ProvisioningState:provisioningState}" \
        --output table
    ```
3. Check logs
    ```bash
    az container logs \
        --resource-group learn-deploy-aci-rg \
        --name mycontainer-restart-demo
    ```
4. Attach to container (receive events)
    ```bash
    az container attach \
        --resource-group learn-deploy-aci-rg \
        --name mycontainer
    ```
5. Monitor container (CPUUsage, MemoryUsage)
    ```bash
    az monitor metrics list \
        --resource $CONTAINER_ID \
        --metrics CPUUsage \
        --output table
    ```

## 1.2 Create Azure App Service Web Apps
### create an Azure App Service Web App
### enable diagnostics logging
### deploy code to a web app
### configure web app settings including SSL, API settings, and connection strings
### implement autoscaling rules including scheduled autoscaling and autoscaling by operational or system metrics
## 1.3 Implement Azure functions
### create and deploy Azure Functions apps
### implement input and output bindings for a function
### implement function triggers by using data operations, timers, and webhooks
### implement Azure Durable Functions
### implement custom handlers
