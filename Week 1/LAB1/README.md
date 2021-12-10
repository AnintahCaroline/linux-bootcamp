# Lab 1: Create a Linux virtual machine with the Azure CLI

1. Launch Azure Cloud Shell
2. Create a resource group
3. Create virtual machine
4. Open port 80 for web traffic
5. Connect to virtual machine
6. Install web server
7. View the web server in action

### Notes:

Quickstart: Create a Linux VM
* https://docs.microsoft.com/en-us/azure/virtual-machines/linux/quick-create-cli

Quickstart for Bash in Azure Cloud Shell
* https://docs.microsoft.com/en-us/azure/cloud-shell/quickstart



# THINGS I LEARNT FROM COMPLETING LAB1

## 1 Launching Azure Cloud Shell
Azure Cloud Shell is an interactive, authenticated, browser-accessible shell for managing Azure resources. It provides the flexibility of choosing the shell experience that best suits the way you work, either Bash or PowerShell.

**HOW TO LAUNCH AZURE CLOUD SHELL**
To launch Azure Cloud Shell click on the cloud shell icon on your Azure portal

## 2 Creating a resource group
A resource group is used to categorise your Azure resources based on a specific region. A resource group cannot span across different regions, all resources are grouped regionally.

COMMAND FOR CREATING A RESOURCE GROUP
 ```
 az group create --name caroline --location eastus
 ```
 
## 3 Creating a Virtual Machine
A virtual machine (VM) is a virtual environment that works like a computer within a computer. It provides a computing power necessary to run an application.

COMMAND FOR CREATING A VIRTUAL MACHINE 
  ```
  az vm create --resource-group caroline --name carolinevm --image UbuntuLTS --admin-username caroline --generate-ssh-keys
  ```
  
 ## 4 Opening port 80 for web traffic
Port 80 is the port incharge of http connections. it needs to be open for people on the web to have access to the server. if a VM is created and port 80 is not opened, the IP address will give the connection error.

COMMAND FOR OPENING PORT 80 FOR WEB TRAFFIC
```
az vm open-port --port 80 --resource-group caroline --name carolinevm
```

## 5 Connecting to virtual machine
To connect to a Linux VM a secure shell connection must be established between the local machine and VM instance. To secure an ssh you need to ensure your private key is saved in your local directory.

COMMAND FOR CONNECTING TO A VIRTUAL MACHINE
```
ssh -i privatekey caroline@20.119.36.96
```

## 6 Installing a web server
Once a remote connection is established with the virtual machine, updates need to  be installed on the server. 

COMMAND FOR INSTALLING UPDATE ON A WEB SERVER
```
sudo apt-get -y update
```
To install the web server, you run the following command which downloads and installs apache2
```
sudo apt-get -y apache2
```

## 7 Viewing the web server in action
The webserver can be viewed by going to the IP address of the virtual machine.

