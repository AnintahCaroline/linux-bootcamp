# Lab 4: Manage Packages and Services on a Linux VM (Azure or AWS)

1. Create a Linux VM
2. Install the Apache Web Server
3. Start the service status via command line
4. Investigate the service status via command line
5. Stop the service 

Challenge: Create a boostrapping script that will install and start this service on new EC2 VMs

### Notes:

Install and Configure Apache (Ubuntu)
* https://ubuntu.com/tutorials/install-and-configure-apache#1-overview

How to install Apache on RHEL 8 / CentOS 8 Linux
* https://linuxconfig.org/installing-apache-on-linux-redhat-8

How to use cloud-init to customize a Linux virtual machine in Azure on first boot
* https://docs.microsoft.com/en-us/azure/virtual-machines/linux/tutorial-automate-vm-deployment

Create bootstrap actions to install additional software
* https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-plan-bootstrap.html

# Things learnt from Managing Packages and Services on a Linux VM using AWS


## 1. Creating a Linux Virtual Machine on AWS
A Virtual Machine on AWS is called the elastic cloud compute (EC2). An EC2 instance can be created using AWS console. TO do this the EC2 resource should be selected and then click on create instance, After this, specify the Amazon machine image as well as the instance type and the security group of the EC2 instance.


## 2. Install the Apache Web Server using AWS
Once a remote connection is established with the EC2 instance, updates need to be installed on the server.

**COMMAND FOR UPDATING THE WEBSERVER**
```
sudo yum update-y
```

## 3. Starting the service status via command line using Azure
When a virtual machine stops, the command below can be used to restart it.

**COMMAND FOR STARTING AN AZURE VM**
```
az vm start -n vmname -g RGname --verbose
 ```

## 4. Investigate the service status via command line
The command line used for this is the Azure cloud shell. This is done to identify the state of all virtual machines, they can either be running, stopped, terminated, or de-allocated


## 5. Stop the service 
This is used to stop the Azure vm.
 &#x26A0; Kindly note that when a vm is stopped it will be given a new ip address once it is restarted.

