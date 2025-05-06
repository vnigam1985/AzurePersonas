
# Azure Engineering Personas - Role Responsibilities and Environment-Based Access

This document outlines custom RBAC roles for five Azure personas, aligned with least-privilege and environment-based access control.

---

## 👤 1. Azure Serverless Developer

### 🔧 Responsibilities
- Manage Azure Functions: update app settings, restart apps, test via runtime
- Upload and manage blob/queue data in non-prod environments
- View and debug via Application Insights and Log Analytics
- Read and execute Logic Apps, manage Event Grid subscriptions
- Access secrets from Key Vault
- Raise and monitor Azure support tickets

### 🔐 Environment-Based Access

| Environment | Storage | Function Apps | Logic Apps | Key Vault | Monitoring | Messaging | Support |
|-------------|---------|----------------|------------|------------|------------|-----------|---------|
| Sandbox     | Read/Write | Full RW       | RW         | Read-only | Full       | Full      | Full    |
| Dev         | Read-only  | Read-only     | Read-only  | Read-only | Full       | Full      | Full    |
| Prod        | ❌         | ❌            | ❌         | ❌        | Read-only | ❌        | Read    |

---

## 👤 2. Azure IaaS Engineer

### 🔧 Responsibilities
- Start/stop/restart/resize VMs
- Install VM extensions (e.g., diagnostics)
- Create snapshots and managed images
- Attach/detach/resize disks (no delete)
- Configure and trigger Azure Backup & Restore
- Work with availability sets and VM scale sets
- Read metrics, view diagnostics, access logs
- Reset admin passwords via RunCommand
- Connect via Bastion
- Open and manage support tickets

### 🔐 Environment-Based Access

| Environment | VM Control | Disks & Images | Backup | Extensions | Networking | Monitoring | Bastion | Support |
|-------------|------------|----------------|--------|------------|------------|------------|---------|---------|
| Sandbox     | Full RW    | Full RW        | Full   | RW         | RW         | Full       | Read    | Full    |
| Dev         | RW         | RW             | RW     | RW         | RW         | Full       | Read    | Full    |
| Prod        | PowerOps   | Read-only      | Restore| Install    | Read-only  | Read-only  | Read    | Full    |

---

## 👤 3. Azure Data Engineer

### 🔧 Responsibilities
- Trigger/debug ADF pipelines
- Read/write datasets to blob and file storage
- Read and run Synapse pipelines
- Query Azure SQL databases
- View App Insights and logs for pipelines
- Access secrets from Key Vault
- Interact with messaging resources
- Raise Azure support tickets

### 🔐 Environment-Based Access

| Environment | ADF | Storage | SQL DB | Synapse | Key Vault | Monitoring | Messaging | Support |
|-------------|-----|---------|--------|---------|------------|------------|-----------|---------|
| Sandbox     | RW  | RW      | RW     | RW      | Read-only | Full       | Read      | Full    |
| Dev         | RW  | Read    | RW     | RW      | Read-only | Full       | Read      | Full    |
| Prod        | Trigger | ❌  | Read   | Read-only | Read-only | Read-only | ❌       | Full    |

---

## 👤 4. Azure AI Engineer

### 🔧 Responsibilities
- Train ML models via AML compute
- Manage registered models and environments
- Deploy online/batch endpoints
- Use and monitor Cognitive Services
- Manage dataset access via blob
- Access secrets via Key Vault
- View metrics, logs, and diagnostics
- Raise support requests

### 🔐 Environment-Based Access

| Environment | AML | Storage | Cognitive | Key Vault | Monitoring | Support |
|-------------|-----|---------|-----------|-----------|------------|---------|
| Sandbox     | RW  | RW      | RW        | Read-only | Full       | Full    |
| Dev         | RW  | Read    | RW        | Read-only | Full       | Full    |
| Prod        | Deploy | ❌   | Read-only | Read-only | Read-only  | Full    |

---

## 👤 5. Azure Crypto Manager

### 🔧 Responsibilities
- Create/manage secrets and keys
- Configure RBAC and access policies in Key Vault
- Share secrets across environments
- Rotate and audit secret usage

### 🔐 Access Across Environments

| Environment | Vault Access | Rotation | Policy Control |
|-------------|--------------|----------|----------------|
| Sandbox     | Full         | Yes      | Yes            |
| Dev         | Full         | Yes      | Yes            |
| Prod        | Full         | Yes      | Yes            |

🛡️ Note: Crypto Manager must remain a dedicated role.

---

## ✅ Notes
- All resource **deployment is handled via SPNs/IaC**.
- All personas work under **environmental scopes**, using `AssignableScopes`.
- No persona has delete rights unless explicitly required for recovery/testing.
