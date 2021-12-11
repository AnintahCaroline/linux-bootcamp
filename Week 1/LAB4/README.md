# Lab 4: Create and use an SSH public-private key pair for Linux VMs in Azure

1. Supported SSH key formats
2. Create an SSH key pair
3. Provide an SSH public key when deploying a VM
4. SSH into your VM

### Notes:

Quickstart: SSH for Linux VMs
* https://docs.microsoft.com/en-us/azure/virtual-machines/linux/mac-create-ssh-keys

Quickstart for Bash in Azure Cloud Shell
* https://docs.microsoft.com/en-us/azure/cloud-shell/quickstart

# THINGS LEARNT FROM LAB 4

## 1. Supported SSH key formats
 SSH keys are used to ensure a secure connection between a remote pc and a virtual machine. SSH keys work in pairs containing two items - pulic and private keys. The SSH key format supported by Azure is  SSH protocol 2 (SSH-2) RSA public-private key pairs with a minimum length of 2048 bits.
 
 ## 2. Create an SSH key pair
 SSH key pairs can be created via the following means
 1. Generating a new key pair during a vm creation
 2. using an SSH client such as putty to generate a new key pair
 
 COMMAND FOR CREATING AN SSH PAIR
 ```
 ssh-keygen -m PEM -t rsa -b 4096
 ```
 
 **OUTPUT**
```
Generating public/private rsa key pair.
Enter file in which to save the key (/home/leena/.ssh/id_rsa): anintah_pem.key
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in anintah_pem.key.
Your public key has been saved in anintah_pem.key.pub.
The key fingerprint is:
SHA256:HCj0ABnRcZRjnPg2Il/2TANf8e2sYH3qTVNkY20LArI leena@cc-52b8c665-669d55595-v8vj7
The key's randomart image is:
+---[RSA 4096]----+
|  +*+=o+ ...     |
|  ..o+B.o o. .  .|
|    .ooE.. ....o=|
|  . ..*.+. ..oo+o|
|   o = =S.o . +..|
|    .   o. . + . |
|            o o  |
|           . o . |
|            . .  |
+----[SHA256]-----+
```

## 3. Provide an SSH public key when deploying a VM

When an instance is created, An already existing SSH key can be used to bconnect to the VM
COMMAND TO PROVIDE AN SSH PUBLIC KEY WHEN DEPLOYING A VM
```
az vm create --resource-group carolineDisk --name carolineVM --image UbuntuLTS --admin-username anintah --ssh-key-values mysshkey.pub
```
## 4. SSH into your VM
To connect to a Linux VM a secure shell connection must be established between the local machine and VM instance. To secure an ssh you need to ensure your private key is saved in your local directory.
