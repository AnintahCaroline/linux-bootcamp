# Lab 3: Manage Azure disks with the Azure CLI

1. Default Azure disks
2. Azure data disks
3. VM disk types
4. Launch Azure Cloud Shell
5. Create and attach disks
6. Prepare data disks
7. Take a disk snapshot

### Notes:

Quickstart: Manage Azure disks
* https://docs.microsoft.com/en-us/azure/virtual-machines/linux/tutorial-manage-disks

Quickstart for Bash in Azure Cloud Shell
* https://docs.microsoft.com/en-us/azure/cloud-shell/quickstart

# THINGS LEARNT FROM LAB 3 

## 1. Defult Azure disks
When ever a new vm is created, Azure automatically allocates data volumes to the new vm. 

COMMAND FOR ATTACHING DISK AT VM CREATION
```
az group create --name carolineDisk --location eastus
```

## 2. Azure data disks
These are storage volumess which are attached to a virtual machine. They provide persistence of data. This means data is not lost whenever a virtual machine is stopped. Data disks also provide storage space for Azure Cloud Shell to run.

COMMAND TO ATTACH DISK TO EXISTING VM
```
  az vm disk attach     --resource-group carolineDisk     --vm-name carolineVM     --name carolineDataDisk     --size-gb 128     --sku Premium_LRS     --new
```

## 3. VM disk types
 There are various disk types/sizes which work best depending on the use of the virtual machine. 
 Some disks are storage optimized, speed optimized and power optimized.

## 4. Launch Azure Cloud Shell
Azure Cloud Shell is an interactive, authenticated, browser-accessible shell for managing Azure resources. It provides the flexibility of choosing the shell experience that best suits the way you work, either Bash or PowerShell.

**HOW TO LAUNCH AZURE CLOUD SHELL**

To launch Azure Cloud Shell click on the cloud shell icon on your Azure portal

## 5. Create and attach disks
A disk can be attace while creating a vm, this is to provide additional storage to ru software applications on the server

COMMAND FOR ATTACHING DISK TO EXISTING VM
```
az vm disk attach     --resource-group carolineDisk     --vm-name carolineVM     --name carolineDataDisk     --size-gb 128     --sku Premium_LRS     --new
```

## 6. Prepare data disks
After a disc is created it is neccessary to  configure it so it can function optimally with the virtual machine

## 7. Take a disk snapshot
Taking a disk snapshot means to capture the current hardware and software configurations of the virtual machine as well as its operating system. A snapshot can be used to replicate identical servers on demand in auto auto scaling groups.
COMMAND FOR CREATING A SNAPSHOT
```
osdiskid=$(az vm show --resource-group carolineDisk --name carolineVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
```
