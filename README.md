# AzurePersonas
This repo contains various Azure Personas Custom RBAC roles, which will serve specific category of cloud engineers

# Serverless Developer - Granular Access

**Description**:  
Granular permissions for serverless developers to manage Azure Functions, App Service Plans, ASEs, monitoring, and storage accounts post-initial deployment.  
No resource creation or deletion is allowed — only updates, testing, configuration, and troubleshooting.

## Allowed Actions:
- Manage app settings, connection strings, functions
- Restart/start/stop sites and slots
- Read and adjust App Service Plans (scale up/down)
- Read App Service Environments
- Monitor insights, diagnostics, and logs
- Read Key Vault secrets
- Read and operate on storage blobs and queues
- Manage Event Grid subscriptions
- Run and troubleshoot Logic Apps
- Open and manage Azure Support tickets

## Data Actions:
- Read, write, and delete blobs
- Manage queue messages
- Query Log Analytics

## Assignable Scope:
- Specific subscription only

---

# Azure IaaS Engineer - Custom RBAC Role

## Purpose
Granular, least-privilege role for Azure IaaS engineers allowing management and troubleshooting of compute, networking, storage, monitoring, and support tasks without giving owner/admin rights.

---

## Permissions

### Compute (VMs)
- Read VM properties
- Start, Stop, Restart, Deallocate VMs
- Resize VMs (SKU change)
- Run VM commands
- View Instance health (instanceView)

### Disks & Snapshots
- Read/Write managed disks
- Access snapshots

### Networking
- Read/Write NICs (incl. IP configuration)
- Read Public IPs
- Read Virtual Networks and Subnets
- Read/Write NSG rules
- Read Load Balancers and backend pools

### Azure Bastion
- Read Bastion resources
- Start Bastion session

### Monitoring
- View Diagnostic settings
- View Metric Alerts
- View Application Insights components
- View Queries
- View Autoscale settings

### Storage
- Read Storage Accounts
- Read/List containers
- Read/Write/Delete blobs

### Logs & Support
- Query Log Analytics workspaces
- Create and View Azure Support Tickets

### Resource Groups and Tags
- Read Resource Groups
- Read and Write Tags

---

## Notes
- Initial infrastructure deployment (VMs, VNets, etc.) happens via Infrastructure-as-Code (IaC) tools like Terraform/Bicep.
- Engineer role focuses on operations, monitoring, troubleshooting, and minor updates only.
- No delete permission for VMs or critical resources.

---

## Scope
- Assignable Scope: `/subscriptions/{subscription-id}`

---


# Azure Data Engineer - Custom RBAC Role

## Purpose
Granular, least-privilege role for Azure Data Engineers to manage and troubleshoot data pipelines, storage, databases, and monitoring without needing full control.

---

## Permissions

### Azure Data Factory (ADF)
- Read pipelines
- Trigger/debug pipelines
- Read datasets and linked services
- Start/Stop triggers

### Azure Synapse Analytics
- Read Synapse Workspaces and Pipelines
- Trigger pipeline runs
- Read SQL Pools

### Azure SQL
- Read SQL servers and databases
- Execute queries
- Read auditing settings

### Storage (Blob & File)
- Read/Write/Delete blobs and files
- Read containers and shares
- List storage account keys

### Monitoring
- View Diagnostics, Metric Alerts, Application Insights
- Query Log Analytics workspaces

### Key Vault
- Read Vault properties
- Get secret values

### Messaging
- Read Event Hubs namespaces and hubs
- Read Service Bus namespaces and queues

### Support
- Create and View Azure Support Tickets

---

## Notes
- Initial resource deployments (Data Factory, Synapse, Storage) are handled via IaC (Terraform, Bicep).
- Engineer role focuses on runtime operations, pipeline execution, storage interaction, and monitoring.
- No delete access for critical Azure services themselves (only data level deletes allowed).

---

## Scope
- Assignable Scope: `/subscriptions/{subscription-id}`

---

# Custom Azure AI Engineer Role

## Description
Custom RBAC Role for Azure AI Engineers with only essential permissions, enabling them to manage Machine Learning, Cognitive Services, Storage, Key Vault, Monitoring, and Support scenarios — without full deployment control.

---

## Included Permissions

### Azure Machine Learning Services
- Read Workspace Properties
- Read Notebooks
- Read Compute Targets
- Start and Stop Compute Instances
- Read Registered Models
- Read Endpoint Deployments

### Azure Storage
- Read Storage Account Properties
- List Storage Keys
- Read blobs (model/data assets)

### Azure Key Vault
- Read Vault Properties
- Read and List Secrets

### Azure Cognitive Services
- Read Cognitive Services Account Properties
- List Access Keys
- Regenerate Access Keys
- Read Deployment Details
- Read Metrics and Usage Data

### Azure Monitor
- Read Alerts
- Read Metrics
- Read Diagnostic Settings

### Azure Support
- Read Support Tickets
- Create Support Tickets

---

## Important Notes
- **No resource creation or deletion** permissions granted.
- **All critical deployments** (AML workspace, storage account creation, cognitive service provisioning) must happen via **Infrastructure as Code (IaC)**.
- **Developer focus** is on configuration changes, running tests, troubleshooting, and monitoring.

---

## Scope
- Assignable Scope: `/subscriptions/{subscription-id}`


