# Lab 2: Manage Linux VMs with the Azure CLI

1. Create resource group
2. Create virtual machine
3. Connect to VM
4. Understand VM images
5. Understand VM sizes
6. VM power states
7. Management tasks

### Notes:

Quickstart: Create a Linux VM
* https://docs.microsoft.com/en-us/azure/virtual-machines/linux/tutorial-manage-vm

Quickstart for Bash in Azure Cloud Shell
* https://docs.microsoft.com/en-us/azure/cloud-shell/quickstart

# THINGS LEARNT FROM LAB2

## 1 Creating a resource group
A resource group is used to categorise your Azure resources based on a specific region. A resource group cannot span across different regions, all resources are grouped regionally.

COMMAND FOR CREATING A RESOURCE GROUP
```
az group create --name caroline --location eastus
```
## 2 Creating a Virtual Machine
A virtual machine (VM) is a virtual environment that works like a computer within a computer. It provides a computing power necessary to run an application.

COMMAND FOR CREATING A VIRTUAL MACHINE
```
az vm create --resource-group caroline --name carolinevm --image UbuntuLTS --admin-username caroline --generate-ssh-keys
```
## 3 Connecting to virtual machine
To connect to a Linux VM a secure shell connection must be established between the local machine and VM instance. To secure an ssh you need to ensure your private key is saved in your local directory.

COMMAND FOR CONNECTING TO A VIRTUAL MACHINE
```
ssh -i privatekey caroline@20.119.36.96
```

## 4 Understanding vm images
VM images are snapshots of operating systems which are loaded unto virtual machines, they provide the basic software infrastructure for a code or application to run on a virtual machine. examples of vm images include; UbuntuLTS, CentOS and Windows Server.

COMMAND FOR UNDERSTANDING VM IMAGES
```
az vm image list --output table
```

## 5 Understanding vm sizes
VM size is the storage space that a vm has. This determines the amount of data it can accomodate and its computing power. 


Example:



MaxDataDiskCount    MemoryInMb    Name                    NumberOfCores    OsDiskSizeInMb    ResourceDiskSizeInMb
------------------  ------------  ----------------------  ---------------  ----------------  ----------------------
2                   512           Standard_B1ls           1                1047552           4096
2                   2048          Standard_B1ms           1                1047552           4096
2                   1024          Standard_B1s            1                1047552           4096
4                   8192          Standard_B2ms           2                1047552           16384
4                   4096          Standard_B2s            2                1047552           8192
8                   16384         Standard_B4ms           4                1047552           32768
16                  32768         Standard_B8ms           8                1047552           65536
16                  49152         Standard_B12ms          12               1047552           98304


COMMAND FOR UNDERSTANDING VM SIZES
```
az vm list-sizes --location eastus --output table
```

## 6  VM power states
This refers to the operation status of a virual machine. The various power state include:
* Running: This state means the virtual machine is in operation, during this state, an instance is billed normally
* Terminated: This is the state which the instance is stopped and can not be resumed
* De-allocated: During this state, the vm is not connected to any storage volume; it is in a detached state.
* Stopped: During this state, the vm is no longer running. Once restarted, it is given a new IP address.

COMMANDS FOR VM POWER STATES
```
az vm stop --resource-group carolineVM --name carolineVM
```
```
 az vm start --resource-group carolineVM --name carolineVM
```

## 7. Management tasks
This refers to the various commands used to manage the AWS resources.
