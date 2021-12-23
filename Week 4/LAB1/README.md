# Lab 1: Deploy a container instance in Azure using the Azure CLI

1. Create a resource group
2. Create a container
3. Pull the container logs
4. Attach output streams
5. Clean up resources

### Notes:

Quickstart: Deploy a container instance in Azure using the Azure CLI
* https://docs.microsoft.com/en-us/azure/container-instances/container-instances-quickstart


# Things learnt in the process of Deploying a container instance in Azure using the Azure CLI

## 1. Create a resource group
 Resource groups allow you to organize and manage related Azure resources.

**Command for creating a resource group**
```
az group create --name myResourceGroup --location eastus
```
```
Output

{
  "id": "/subscriptions/c40f76f6-a340-40f3-930a-cdba85821538/resourceGroups/caroline",
  "location": "eastus",
  "managedBy": null,
  "name": "caroline",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null,
  "type": "Microsoft.Resources/resourceGroups"
}
```
