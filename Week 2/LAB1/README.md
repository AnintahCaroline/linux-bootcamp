# Lab 1: Create a Linux virtual machine with the AWS CLI

1. Launch AWS Cloud Shell
2. Create virtual machine
3. Open port 80 for web traffic
4. Connect to virtual machine
5. Install web server
6. View the web server in action

### Notes:

Quickstart: Create a Linux VM
* https://aws.amazon.com/getting-started/launch-a-virtual-machine-B-0/

Quickstart for AWS CloudShell
* https://docs.aws.amazon.com/cloudshell/latest/userguide/working-with-cloudshell.html

# THINGS I LEARNT FROM COMPLETING LAB 1

## 1. Launching AWS Cloud Shell
AWS cloud shell is an integrated browser based scripting environment. It works with the AWSCLI to give access to commands which can be used to control AWS resources. AWS cloud shell has a persistant storage attached. This means there is 1gig  free storage to store programs and applications. To launch the cloud shell, click on the cloud shell icon at the top navigation bar of the AWS console.


## 2. Creating a Virtual Machine
A Virtual Machine on AWS is called the elastic cloud compute (EC2). An EC2 instance can be created using AWS console. TO do this the EC2 resource should be selected and then  click on create instance, After this, specify the Amazon machine image as well as the instance type and the security group of the EC2 instance.


## 3. Open port 80 for web traffic
Port 80 is the port incharge of http connections. it needs to be open for people on the web to have access to the server. if an EC2 instance is created and port 80 is not opened, the IP address will give the connection error. To Open up port 80, an http security needs to be attached to the EC2 instance. This allows public http access.


## 4. Connect to virtual machine
To connect to an EC2 instance, a secure shell connection must be established between the local machine and the EC2instance. To secure an ssh you need to ensure your private key is saved in your local directory.

** COMMAND FOR CONNECTING TO A VM **

```
ssh -i privatekey.pem ec2ipaddress
```

## 5. Install web server
Once a remote connection is established with the EC2 instance, updates need to be installed on the server.
 
 ** COMMAND FOR UPDATING THE WEBSERVER**
 
 ```
 sudo yum update-y
 ```

** COMMAND FOR INSTALLING APACHE WEB SERVER **

```
sudo yum install apache2
```

## 6. View the web server in action6. View the web server in action
The webserver can be viewed by going to the IP address of the Elastic Cloud Compute (EC2) instance
