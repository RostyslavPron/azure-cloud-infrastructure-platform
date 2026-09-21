# Azure Cloud Shell Automation

## Project Overview

Azure Cloud Shell was used to automate the deployment, administration, and validation of cloud infrastructure resources. Using Azure CLI enabled a consistent, repeatable workflow for managing Azure services while reducing manual configuration tasks.

## Business Objective

The objective was to establish an operational workflow capable of:

- Deploying Azure resources efficiently
- Managing infrastructure through command-line automation
- Validating resource configurations
- Supporting Infrastructure as Code deployments
- Improving deployment consistency and operational efficiency

---

# Solution Architecture

Azure Cloud Shell served as the primary administration environment for:

- Resource Group Management
- Infrastructure Deployment
- Azure Function Administration
- Network Security Validation
- Key Vault Management
- Resource Monitoring

---

# Environment Verification

## Verify Active Azure Subscription

```bash
az account show
```

### Description

Displays the currently authenticated Azure subscription and tenant information.

### Outcome

Confirmed access to the target Azure subscription before resource deployment.

---

## List Available Subscriptions

```bash
az account list --output table
```

### Description

Displays all available Azure subscriptions associated with the account.

### Outcome

Verified the correct subscription was selected for deployment activities.

---

# Resource Group Management

## Create Resource Group

```bash
az group create \
    --name rg-cloud-platform \
    --location eastus
```

### Description

Creates a resource group used to organize infrastructure components.

### Outcome

Successfully provisioned a centralized container for all project resources.

---

## Verify Resource Group

```bash
az group show \
    --name rg-cloud-platform
```

### Description

Validates that the resource group was successfully created.

### Outcome

Confirmed successful deployment and configuration.

---

# Infrastructure as Code Deployment

## Validate ARM Template

```bash
az deployment group validate \
    --resource-group rg-cloud-platform \
    --template-file template.json
```

### Description

Performs a validation check against the ARM template before deployment.

### Benefits

- Detects configuration issues early
- Reduces deployment failures
- Improves infrastructure reliability

---

## Deploy ARM Template

```bash
az deployment group create \
    --resource-group rg-cloud-platform \
    --template-file template.json
```

### Description

Deploys Azure resources using Infrastructure as Code principles.

### Benefits

- Repeatable deployments
- Version-controlled infrastructure
- Reduced configuration drift

---

# Azure Function Deployment

## Create Storage Account

```bash
az storage account create \
    --name cloudplatformstorage01 \
    --resource-group rg-cloud-platform \
    --location eastus \
    --sku Standard_LRS
```

### Description

Creates storage required by the Azure Function App.

### Outcome

Provisioned storage services supporting serverless operations.

---

## Create Azure Function App

```bash
az functionapp create \
    --resource-group rg-cloud-platform \
    --consumption-plan-location eastus \
    --runtime dotnet \
    --functions-version 4 \
    --name cloud-platform-function \
    --storage-account cloudplatformstorage01
```

### Description

Deploys a serverless Function App within Azure.

### Benefits

- Automatic scaling
- Reduced operational overhead
- Consumption-based pricing model

---

## Verify Function App

```bash
az functionapp show \
    --name cloud-platform-function \
    --resource-group rg-cloud-platform
```

### Description

Retrieves Function App configuration and status information.

### Outcome

Confirmed successful deployment and availability.

---

# Network Security Administration

## List Network Security Groups

```bash
az network nsg list \
    --resource-group rg-cloud-platform \
    --output table
```

### Description

Displays Network Security Groups associated with the environment.

### Outcome

Verified security controls were successfully deployed.

---

## Review Security Rules

```bash
az network nsg rule list \
    --resource-group rg-cloud-platform \
    --nsg-name platform-nsg \
    --output table
```

### Description

Displays inbound and outbound security rules.

### Outcome

Validated implementation of least-privilege access policies.

---

# Azure Key Vault Management

## Create Key Vault

```bash
az keyvault create \
    --name kv-cloud-platform \
    --resource-group rg-cloud-platform \
    --location eastus
```

### Description

Creates a centralized service for secure secret storage.

### Benefits

- Enhanced security posture
- Centralized credential management
- Reduced exposure of sensitive information

---

## Store Secret

```bash
az keyvault secret set \
    --vault-name kv-cloud-platform \
    --name DatabasePassword \
    --value "ExamplePassword123"
```

### Description

Stores sensitive data securely within Key Vault.

### Outcome

Credentials were protected from exposure within application code and configuration files.

---

## Retrieve Secret

```bash
az keyvault secret show \
    --vault-name kv-cloud-platform \
    --name DatabasePassword
```

### Description

Retrieves secret information for validation purposes.

### Outcome

Confirmed successful secret storage and retrieval.

---

# Resource Inventory and Monitoring

## List Resources

```bash
az resource list \
    --resource-group rg-cloud-platform \
    --output table
```

### Description

Displays all deployed resources within the resource group.

### Outcome

Generated a complete inventory of deployed infrastructure.

---

## Monitor Resource Health

```bash
az resource list \
    --resource-group rg-cloud-platform \
    --query "[].{Name:name,Type:type}" \
    --output table
```

### Description

Provides a simplified view of deployed resources.

### Outcome

Validated successful deployment of cloud components.

---

# Validation Checklist

The following validation activities were completed:

- [x] Azure subscription verified
- [x] Resource group created
- [x] ARM template validated
- [x] Infrastructure deployed successfully
- [x] Storage account provisioned
- [x] Azure Function App deployed
- [x] Network security verified
- [x] Azure Key Vault configured
- [x] Secrets stored securely
- [x] Resource inventory validated

---

# Results

Azure Cloud Shell and Azure CLI were successfully used to automate infrastructure administration tasks throughout the project lifecycle. The implementation demonstrated the practical application of cloud automation, Infrastructure as Code, serverless deployment, security administration, and operational monitoring within Microsoft Azure.

Key outcomes included:

- Faster infrastructure deployment
- Improved configuration consistency
- Enhanced security management
- Streamlined operational workflows
- Increased deployment reliability

---

# Skills Demonstrated

- Microsoft Azure
- Azure CLI
- Azure Cloud Shell
- Infrastructure as Code (IaC)
- Resource Administration
- Cloud Automation
- Serverless Computing
- Azure Functions
- Azure Key Vault
- Network Security
- Azure Resource Management
- Cloud Operations
