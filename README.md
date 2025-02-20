# gesda-infrastructure

Top level infrastructure for the GESDA project resources to host.


Steps to create service connection to access storage account to manage infrastructure templates from CICD pipeline on Azure DevOps

Create Storage Account with 'AzureBlob' support.

#### 1. Login to Azure
az login

#### 2. Create Service Principal and save output to variable
```
az ad sp create-for-rbac --name "YourServicePrincipalName" --role "Storage Blob Data Contributor" --scope /subscriptions/{SubscriptionId}/resourceGroups/{ResourceGroupName}/providers/Microsoft.Storage/storageAccounts/{StorageAccountName}
```


The command will output something like this (save these values):


```
{
  "appId": "xxxxx-xxxxx-xxxxx-xxxxx",
  "displayName": "YourServicePrincipalName",
  "password": "xxxxx-xxxxx-xxxxx-xxxxx",
  "tenant": "xxxxx-xxxxx-xxxxx-xxxxx"
}
```

#### 3. In Azure DevOps, create a Service Connection

- Go to Project Settings → Service Connections
- Click "New Service Connection"
- Select "Azure Resource Manager"
- Choose "Service Principal (manual)"
- Fill in the details:

    - Subscription ID
    - Subscription Name
    - Service Principal ID (appId)
    - Service Principal Key (password)
    - Tenant ID (tenant)

- Give your service connection a name (e.g., "azure-storage-connection")


#### 4. Update your pipeline YAML with the service connection:

