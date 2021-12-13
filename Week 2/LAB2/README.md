# Lab 2: Manage Linux VMs with the AWS CLI

1. Create virtual machine
2. Connect to VM
3. Understand VM images
4. Understand VM sizes
5. VM power states
6. Management tasks

### Notes:

Quickstart: Create a Linux VM
* https://aws.amazon.com/getting-started/launch-a-virtual-machine-B-0/

Using a custom Amazon machine image (AMI)
* https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/using-features.customenv.html

Quickstart: Restart VM via CLI
* https://docs.aws.amazon.com/cli/latest/reference/ec2/reboot-instances.html

Quickstart for AWS CloudShell
* https://docs.aws.amazon.com/cloudshell/latest/userguide/working-with-cloudshell.html

# THINGS LEARNT FROM WORKING ON LAB 2

## 1. Creating a Virtual Machine
A Virtual Machine on AWS is called the elastic cloud compute (EC2). An EC2 instance can be created using AWS console. TO do this the EC2 resource should be selected and then click on create instance, After this, specify the Amazon machine image as well as the instance type and the security group of the EC2 instance.


## 2. Connect to virtual machine
To connect to an EC2 instance, a secure shell connection must be established between the local machine and the EC2instance. To secure an ssh you need to ensure your private key is saved in your local directory.

**COMMAND FOR CONNECTING TO A VM**

```
ssh -i privatekey.pem ec2ipaddress
```


## 3. Understand VM images
In AWS, vm images are called Amazon machine images (AMI). AMI's are formed from snapshots of the EC2 operatings systems and hardware configurations. They are used to easily spin up new  identical EC2 instances when the demand arises. 


##  4. Understand VM sizes


