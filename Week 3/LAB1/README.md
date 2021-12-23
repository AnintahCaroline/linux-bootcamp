# Lab 1: Install a LAMP stack on an Azure Linux VM

1. Create a resource group
2. Create a virtual machine
3. Open port 80 for web traffic
4. SSH into your VM
5. Install Apache, MySQL, and PHP
6. Install WordPress

### Notes:

Tutorial: Install a LAMP stack on an Azure Linux VM
* https://docs.microsoft.com/en-us/azure/virtual-machines/linux/tutorial-lamp-stack

Sample Gist
* https://gist.github.com/mikepfeiffer/96d659042f0575a617648a33c92b8f4a

Build and run a web application with the MEAN stack on an Azure Linux virtual machine
* https://docs.microsoft.com/en-us/learn/modules/build-a-web-app-with-mean-on-a-linux-vm/

MEAN Stack App
* https://github.com/MicrosoftDocs/mslearn-build-a-web-app-with-mean-on-a-linux-vm

# THINGS LEARNT FROM INSTALLING A LAMP STACK ON AN AZURE LINUX VM

## 1. Creating a resource group

A resource group is used to categorise your Azure resources based on a specific region. A resource group cannot span across different regions, all resources are grouped regionally.

**COMMAND FOR CREATING A RESOURCE GROUP**
```
az group create --name caroline --location eastus
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
## 2. Creating a Virtual Machine

A virtual machine (VM) is a virtual environment that works like a computer within a computer. It provides a computing power necessary to run an application.

**COMMAND FOR CREATING A VIRTUAL MACHINE**
```
az vm create --resource-group caroline --name carolinevm --image UbuntuLTS --admin-username caroline --generate-ssh-keys
```

```
Output

{
  "fqdns": "",
  "id": "/subscriptions/c40f76f6-a340-40f3-930a-cdba85821538/resourceGroups/caroline/providers/Microsoft.Compute/virtualMachines/carolinevm",
  "location": "eastus",
  "macAddress": "00-22-48-1F-C6-09",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "20.127.92.128",
  "resourceGroup": "caroline",
  "zones": ""
}
```
## 3. Opening port 80 for web traffic

**Command for opening porT 80**
```
az vm open-port --port 80 --resource-group caroline  --name carolinevm
```
```
Output

{
  "defaultSecurityRules": [
    {
      "access": "Allow",
      "description": "Allow inbound traffic from all VMs in VNET",
      "destinationAddressPrefix": "VirtualNetwork",
      "destinationAddressPrefixes": [],
      "destinationApplicationSecurityGroups": null,
      "destinationPortRange": "*",
      "destinationPortRanges": [],
      "direction": "Inbound",
      "etag": "W/\"dc659de6-329c-44ac-abae-03abf495a5de\"",
      "id": "/subscriptions/c40f76f6-a340-40f3-930a-cdba85821538/resourceGroups/caroline/providers/Microsoft.Network/networkSecurityGroups/carolinevmNSG/defaultSecurityRules/AllowVnetInBound",
      "name": "AllowVnetInBound",
      "priority": 65000,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "caroline",
      "sourceAddressPrefix": "VirtualNetwork",
      "sourceAddressPrefixes": [],
      "sourceApplicationSecurityGroups": null,
      "sourcePortRange": "*",
      "sourcePortRanges": [],
      "type": "Microsoft.Network/networkSecurityGroups/defaultSecurityRules"
    },
    {
      "access": "Allow",
      "description": "Allow inbound traffic from azure load balancer",
      "destinationAddressPrefix": "*",
      "destinationAddressPrefixes": [],
      "destinationApplicationSecurityGroups": null,
      "destinationPortRange": "*",
      "destinationPortRanges": [],
      "direction": "Inbound",
      "etag": "W/\"dc659de6-329c-44ac-abae-03abf495a5de\"",
      "id": "/subscriptions/c40f76f6-a340-40f3-930a-cdba85821538/resourceGroups/caroline/providers/Microsoft.Network/networkSecurityGroups/carolinevmNSG/defaultSecurityRules/AllowAzureLoadBalancerInBound",
      "name": "AllowAzureLoadBalancerInBound",
      "priority": 65001,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "caroline",
      "sourceAddressPrefix": "AzureLoadBalancer",
      "sourceAddressPrefixes": [],
      "sourceApplicationSecurityGroups": null,
      "sourcePortRange": "*",
      "sourcePortRanges": [],
      "type": "Microsoft.Network/networkSecurityGroups/defaultSecurityRules"
    },
    {
      "access": "Deny",
      "description": "Deny all inbound traffic",
      "destinationAddressPrefix": "*",
      "destinationAddressPrefixes": [],
      "destinationApplicationSecurityGroups": null,
      "destinationPortRange": "*",
      "destinationPortRanges": [],
      "direction": "Inbound",
      "etag": "W/\"dc659de6-329c-44ac-abae-03abf495a5de\"",
      "id": "/subscriptions/c40f76f6-a340-40f3-930a-cdba85821538/resourceGroups/caroline/providers/Microsoft.Network/networkSecurityGroups/carolinevmNSG/defaultSecurityRules/DenyAllInBound",
      "name": "DenyAllInBound",
      "priority": 65500,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "caroline",
      "sourceAddressPrefix": "*",
      "sourceAddressPrefixes": [],
      "sourceApplicationSecurityGroups": null,
      "sourcePortRange": "*",
      "sourcePortRanges": [],
      "type": "Microsoft.Network/networkSecurityGroups/defaultSecurityRules"
    },
    {
      "access": "Allow",
      "description": "Allow outbound traffic from all VMs to all VMs in VNET",
      "destinationAddressPrefix": "VirtualNetwork",
      "destinationAddressPrefixes": [],
      "destinationApplicationSecurityGroups": null,
      "destinationPortRange": "*",
      "destinationPortRanges": [],
      "direction": "Outbound",
      "etag": "W/\"dc659de6-329c-44ac-abae-03abf495a5de\"",
      "id": "/subscriptions/c40f76f6-a340-40f3-930a-cdba85821538/resourceGroups/caroline/providers/Microsoft.Network/networkSecurityGroups/carolinevmNSG/defaultSecurityRules/AllowVnetOutBound",
      "name": "AllowVnetOutBound",
      "priority": 65000,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "caroline",
      "sourceAddressPrefix": "VirtualNetwork",
      "sourceAddressPrefixes": [],
      "sourceApplicationSecurityGroups": null,
      "sourcePortRange": "*",
      "sourcePortRanges": [],
      "type": "Microsoft.Network/networkSecurityGroups/defaultSecurityRules"
    },
    {
      "access": "Allow",
      "description": "Allow outbound traffic from all VMs to Internet",
      "destinationAddressPrefix": "Internet",
      "destinationAddressPrefixes": [],
      "destinationApplicationSecurityGroups": null,
      "destinationPortRange": "*",
      "destinationPortRanges": [],
      "direction": "Outbound",
      "etag": "W/\"dc659de6-329c-44ac-abae-03abf495a5de\"",
      "id": "/subscriptions/c40f76f6-a340-40f3-930a-cdba85821538/resourceGroups/caroline/providers/Microsoft.Network/networkSecurityGroups/carolinevmNSG/defaultSecurityRules/AllowInternetOutBound",
      "name": "AllowInternetOutBound",
      "priority": 65001,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "caroline",
      "sourceAddressPrefix": "*",
      "sourceAddressPrefixes": [],
      "sourceApplicationSecurityGroups": null,
      "sourcePortRange": "*",
      "sourcePortRanges": [],
      "type": "Microsoft.Network/networkSecurityGroups/defaultSecurityRules"
    },
    {
      "access": "Deny",
      "description": "Deny all outbound traffic",
      "destinationAddressPrefix": "*",
      "destinationAddressPrefixes": [],
      "destinationApplicationSecurityGroups": null,
      "destinationPortRange": "*",
      "destinationPortRanges": [],
      "direction": "Outbound",
      "etag": "W/\"dc659de6-329c-44ac-abae-03abf495a5de\"",
      "id": "/subscriptions/c40f76f6-a340-40f3-930a-cdba85821538/resourceGroups/caroline/providers/Microsoft.Network/networkSecurityGroups/carolinevmNSG/defaultSecurityRules/DenyAllOutBound",
      "name": "DenyAllOutBound",
      "priority": 65500,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "caroline",
      "sourceAddressPrefix": "*",
      "sourceAddressPrefixes": [],
      "sourceApplicationSecurityGroups": null,
      "sourcePortRange": "*",
      "sourcePortRanges": [],
      "type": "Microsoft.Network/networkSecurityGroups/defaultSecurityRules"
    }
  ],
  "etag": "W/\"dc659de6-329c-44ac-abae-03abf495a5de\"",
  "flowLogs": null,
  "id": "/subscriptions/c40f76f6-a340-40f3-930a-cdba85821538/resourceGroups/caroline/providers/Microsoft.Network/networkSecurityGroups/carolinevmNSG",
  "location": "eastus",
  "name": "carolinevmNSG",
  "networkInterfaces": [
    {
      "dnsSettings": null,
      "dscpConfiguration": null,
      "enableAcceleratedNetworking": null,
      "enableIpForwarding": null,
      "etag": null,
      "extendedLocation": null,
      "hostedWorkloads": null,
      "id": "/subscriptions/c40f76f6-a340-40f3-930a-cdba85821538/resourceGroups/caroline/providers/Microsoft.Network/networkInterfaces/carolinevmVMNic",
      "ipConfigurations": null,
      "location": null,
      "macAddress": null,
      "migrationPhase": null,
      "name": null,
      "networkSecurityGroup": null,
      "nicType": null,
      "primary": null,
      "privateEndpoint": null,
      "privateLinkService": null,
      "provisioningState": null,
      "resourceGroup": "caroline",
      "resourceGuid": null,
      "tags": null,
      "tapConfigurations": null,
      "type": null,
      "virtualMachine": null,
      "vnetEncryptionSupported": null,
      "workloadType": null
    }
  ],
  "provisioningState": "Succeeded",
  "resourceGroup": "caroline",
  "resourceGuid": "6d8aef2e-c443-4523-8f4a-24791b108c9f",
  "securityRules": [
    {
      "access": "Allow",
      "description": null,
      "destinationAddressPrefix": "*",
      "destinationAddressPrefixes": [],
      "destinationApplicationSecurityGroups": null,
      "destinationPortRange": "22",
      "destinationPortRanges": [],
      "direction": "Inbound",
      "etag": "W/\"dc659de6-329c-44ac-abae-03abf495a5de\"",
      "id": "/subscriptions/c40f76f6-a340-40f3-930a-cdba85821538/resourceGroups/caroline/providers/Microsoft.Network/networkSecurityGroups/carolinevmNSG/securityRules/default-allow-ssh",
      "name": "default-allow-ssh",
      "priority": 1000,
      "protocol": "Tcp",
      "provisioningState": "Succeeded",
      "resourceGroup": "caroline",
      "sourceAddressPrefix": "*",
      "sourceAddressPrefixes": [],
      "sourceApplicationSecurityGroups": null,
      "sourcePortRange": "*",
      "sourcePortRanges": [],
      "type": "Microsoft.Network/networkSecurityGroups/securityRules"
    },
    {
      "access": "Allow",
      "description": null,
      "destinationAddressPrefix": "*",
      "destinationAddressPrefixes": [],
      "destinationApplicationSecurityGroups": null,
      "destinationPortRange": "80",
      "destinationPortRanges": [],
      "direction": "Inbound",
      "etag": "W/\"dc659de6-329c-44ac-abae-03abf495a5de\"",
      "id": "/subscriptions/c40f76f6-a340-40f3-930a-cdba85821538/resourceGroups/caroline/providers/Microsoft.Network/networkSecurityGroups/carolinevmNSG/securityRules/open-port-80",
      "name": "open-port-80",
      "priority": 900,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "caroline",
      "sourceAddressPrefix": "*",
      "sourceAddressPrefixes": [],
      "sourceApplicationSecurityGroups": null,
      "sourcePortRange": "*",
      "sourcePortRanges": [],
      "type": "Microsoft.Network/networkSecurityGroups/securityRules"
    }
  ],
  "subnets": null,
  "tags": {},
  "type": "Microsoft.Network/networkSecurityGroups"
  ```
  
  ## 4. SSH into my VM
  
  **Command to SSH into a VM**
  ```
  ssh caroline@20.127.92.128
  ```
  ```
  Output
  
Welcome to Ubuntu 18.04.6 LTS (GNU/Linux 5.4.0-1064-azure x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Thu Dec 23 20:52:09 UTC 2021

  System load:  0.0               Processes:           108
  Usage of /:   4.6% of 28.90GB   Users logged in:     0
  Memory usage: 5%                IP address for eth0: 10.0.0.4
  Swap usage:   0%

0 updates can be applied immediately.



The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.
```
## 5. Install Apache, MySQL, and PHP
 
 **command for installing  Apache, MySQL, and PHP**
 
 ```
 sudo apt update && sudo apt install lamp-server^
 ```
 ```
 Output
 
Hit:1 http://azure.archive.ubuntu.com/ubuntu bionic InRelease
Get:2 http://azure.archive.ubuntu.com/ubuntu bionic-updates InRelease [88.7 kB]
Get:3 http://azure.archive.ubuntu.com/ubuntu bionic-backports InRelease [74.6 kB]
Get:4 http://security.ubuntu.com/ubuntu bionic-security InRelease [88.7 kB]
Get:5 http://azure.archive.ubuntu.com/ubuntu bionic/universe amd64 Packages [8570 kB]
Get:6 http://azure.archive.ubuntu.com/ubuntu bionic/universe Translation-en [4941 kB]
Get:7 http://azure.archive.ubuntu.com/ubuntu bionic/multiverse amd64 Packages [151 kB]
Get:8 http://azure.archive.ubuntu.com/ubuntu bionic/multiverse Translation-en [108 kB]
Get:9 http://azure.archive.ubuntu.com/ubuntu bionic-updates/main amd64 Packages [2328 kB]
Get:10 http://azure.archive.ubuntu.com/ubuntu bionic-updates/restricted amd64 Packages [559 kB]
Get:11 http://azure.archive.ubuntu.com/ubuntu bionic-updates/universe amd64 Packages [1772 kB]
Get:12 http://azure.archive.ubuntu.com/ubuntu bionic-updates/universe Translation-en [384 kB]
Get:13 http://azure.archive.ubuntu.com/ubuntu bionic-updates/multiverse amd64 Packages [27.3 kB]
Get:14 http://azure.archive.ubuntu.com/ubuntu bionic-updates/multiverse Translation-en [6808 B]
Get:15 http://azure.archive.ubuntu.com/ubuntu bionic-backports/main amd64 Packages [10.3 kB]
Get:16 http://azure.archive.ubuntu.com/ubuntu bionic-backports/main Translation-en [4824 B]
Get:17 http://azure.archive.ubuntu.com/ubuntu bionic-backports/universe amd64 Packages [11.3 kB]
Get:18 http://azure.archive.ubuntu.com/ubuntu bionic-backports/universe Translation-en [5772 B]
Get:19 http://security.ubuntu.com/ubuntu bionic-security/main amd64 Packages [1983 kB]
Get:20 http://security.ubuntu.com/ubuntu bionic-security/main Translation-en [355 kB]
Get:21 http://security.ubuntu.com/ubuntu bionic-security/restricted amd64 Packages [535 kB]
Get:22 http://security.ubuntu.com/ubuntu bionic-security/restricted Translation-en [72.4 kB]
Get:23 http://security.ubuntu.com/ubuntu bionic-security/universe amd64 Packages [1158 kB]
Get:24 http://security.ubuntu.com/ubuntu bionic-security/universe Translation-en [266 kB]
Get:25 http://security.ubuntu.com/ubuntu bionic-security/multiverse amd64 Packages [20.9 kB]
Get:26 http://security.ubuntu.com/ubuntu bionic-security/multiverse Translation-en [4732 B]
Fetched 23.5 MB in 5s (4739 kB/s)
Reading package lists... Done
Building dependency tree
Reading state information... Done
18 packages can be upgraded. Run 'apt list --upgradable' to see them.
Reading package lists... Done
Building dependency tree
Reading state information... Done
Note, selecting 'libgssapi3-heimdal' for task 'lamp-server'
Note, selecting 'libhttp-message-perl' for task 'lamp-server'
Note, selecting 'libnghttp2-14' for task 'lamp-server'
Note, selecting 'php7.2-common' for task 'lamp-server'
Note, selecting 'libencode-locale-perl' for task 'lamp-server'
Note, selecting 'php7.2-cli' for task 'lamp-server'
Note, selecting 'libwind0-heimdal' for task 'lamp-server'
Note, selecting 'libsasl2-modules-db' for task 'lamp-server'
Note, selecting 'mysql-client-5.7' for task 'lamp-server'
Note, selecting 'libldap-2.4-2' for task 'lamp-server'
Note, selecting 'libapache2-mod-php' for task 'lamp-server'
Note, selecting 'libevent-core-2.1-6' for task 'lamp-server'
Note, selecting 'mysql-server-5.7' for task 'lamp-server'
Note, selecting 'php-common' for task 'lamp-server'
Note, selecting 'libaprutil1' for task 'lamp-server'
Note, selecting 'php7.2-mysql' for task 'lamp-server'
Note, selecting 'libheimntlm0-heimdal' for task 'lamp-server'
Note, selecting 'mysql-server' for task 'lamp-server'
Note, selecting 'libcgi-fast-perl' for task 'lamp-server'
Note, selecting 'libwrap0' for task 'lamp-server'
Note, selecting 'libhttp-date-perl' for task 'lamp-server'
Note, selecting 'perl-modules-5.26' for task 'lamp-server'
Note, selecting 'liblwp-mediatypes-perl' for task 'lamp-server'
Note, selecting 'libfcgi-perl' for task 'lamp-server'
Note, selecting 'libheimbase1-heimdal' for task 'lamp-server'
Note, selecting 'libcgi-pm-perl' for task 'lamp-server'
Note, selecting 'libaprutil1-dbd-sqlite3' for task 'lamp-server'
Note, selecting 'libaio1' for task 'lamp-server'
Note, selecting 'php7.2-json' for task 'lamp-server'
Note, selecting 'php7.2-opcache' for task 'lamp-server'
Note, selecting 'libsasl2-2' for task 'lamp-server'
Note, selecting 'libio-html-perl' for task 'lamp-server'
Note, selecting 'ssl-cert' for task 'lamp-server'
Note, selecting 'apache2-data' for task 'lamp-server'
Note, selecting 'libperl5.26' for task 'lamp-server'
Note, selecting 'libapr1' for task 'lamp-server'
Note, selecting 'libaprutil1-ldap' for task 'lamp-server'
Note, selecting 'libhtml-tagset-perl' for task 'lamp-server'
Note, selecting 'mysql-client-core-5.7' for task 'lamp-server'
Note, selecting 'libsasl2-modules' for task 'lamp-server'
Note, selecting 'libldap-common' for task 'lamp-server'
Note, selecting 'php7.2-readline' for task 'lamp-server'
Note, selecting 'libhcrypto4-heimdal' for task 'lamp-server'
Note, selecting 'liblua5.2-0' for task 'lamp-server'
Note, selecting 'mysql-common' for task 'lamp-server'
Note, selecting 'libsodium23' for task 'lamp-server'
Note, selecting 'libhtml-template-perl' for task 'lamp-server'
Note, selecting 'libtimedate-perl' for task 'lamp-server'
Note, selecting 'libroken18-heimdal' for task 'lamp-server'
Note, selecting 'apache2-bin' for task 'lamp-server'
Note, selecting 'perl' for task 'lamp-server'
Note, selecting 'libasn1-8-heimdal' for task 'lamp-server'
Note, selecting 'libkrb5-26-heimdal' for task 'lamp-server'
Note, selecting 'libgdbm-compat4' for task 'lamp-server'
Note, selecting 'apache2' for task 'lamp-server'
Note, selecting 'php-mysql' for task 'lamp-server'
Note, selecting 'apache2-utils' for task 'lamp-server'
Note, selecting 'libhx509-5-heimdal' for task 'lamp-server'
Note, selecting 'libhtml-parser-perl' for task 'lamp-server'
Note, selecting 'libapache2-mod-php7.2' for task 'lamp-server'
Note, selecting 'liburi-perl' for task 'lamp-server'
Note, selecting 'mysql-server-core-5.7' for task 'lamp-server'
libasn1-8-heimdal is already the newest version (7.5.0+dfsg-1).
libasn1-8-heimdal set to manually installed.
libgdbm-compat4 is already the newest version (1.14.1-6).
libgdbm-compat4 set to manually installed.
libgssapi3-heimdal is already the newest version (7.5.0+dfsg-1).
libgssapi3-heimdal set to manually installed.
libhcrypto4-heimdal is already the newest version (7.5.0+dfsg-1).
libhcrypto4-heimdal set to manually installed.
libheimbase1-heimdal is already the newest version (7.5.0+dfsg-1).
libheimbase1-heimdal set to manually installed.
libheimntlm0-heimdal is already the newest version (7.5.0+dfsg-1).
libheimntlm0-heimdal set to manually installed.
libhx509-5-heimdal is already the newest version (7.5.0+dfsg-1).
libhx509-5-heimdal set to manually installed.
libkrb5-26-heimdal is already the newest version (7.5.0+dfsg-1).
libkrb5-26-heimdal set to manually installed.
libnghttp2-14 is already the newest version (1.30.0-1ubuntu1).
libnghttp2-14 set to manually installed.
libroken18-heimdal is already the newest version (7.5.0+dfsg-1).
libroken18-heimdal set to manually installed.
libwind0-heimdal is already the newest version (7.5.0+dfsg-1).
libwind0-heimdal set to manually installed.
libwrap0 is already the newest version (7.6.q-27).
libldap-2.4-2 is already the newest version (2.4.45+dfsg-1ubuntu1.10).
libldap-2.4-2 set to manually installed.
libldap-common is already the newest version (2.4.45+dfsg-1ubuntu1.10).
libldap-common set to manually installed.
libperl5.26 is already the newest version (5.26.1-6ubuntu0.5).
libperl5.26 set to manually installed.
libsasl2-2 is already the newest version (2.1.27~101-g0780600+dfsg-3ubuntu2.3).
libsasl2-2 set to manually installed.
libsasl2-modules is already the newest version (2.1.27~101-g0780600+dfsg-3ubuntu2.3).
libsasl2-modules set to manually installed.
libsasl2-modules-db is already the newest version (2.1.27~101-g0780600+dfsg-3ubuntu2.3).
libsasl2-modules-db set to manually installed.
perl is already the newest version (5.26.1-6ubuntu0.5).
perl set to manually installed.
perl-modules-5.26 is already the newest version (5.26.1-6ubuntu0.5).
perl-modules-5.26 set to manually installed.
The following package was automatically installed and is no longer required:
  linux-headers-4.15.0-163
Use 'sudo apt autoremove' to remove it.
Suggested packages:
  www-browser apache2-doc apache2-suexec-pristine | apache2-suexec-custom php-pear libdata-dump-perl
  libipc-sharedcache-perl libwww-perl mailx tinyca openssl-blacklist
The following NEW packages will be installed:
  apache2 apache2-bin apache2-data apache2-utils libaio1 libapache2-mod-php libapache2-mod-php7.2 libapr1
  libaprutil1 libaprutil1-dbd-sqlite3 libaprutil1-ldap libcgi-fast-perl libcgi-pm-perl libencode-locale-perl
  libevent-core-2.1-6 libfcgi-perl libhtml-parser-perl libhtml-tagset-perl libhtml-template-perl
  libhttp-date-perl libhttp-message-perl libio-html-perl liblua5.2-0 liblwp-mediatypes-perl libsodium23
  libtimedate-perl liburi-perl mysql-client-5.7 mysql-client-core-5.7 mysql-common mysql-server
  mysql-server-5.7 mysql-server-core-5.7 php-common php-mysql php7.2-cli php7.2-common php7.2-json
  php7.2-mysql php7.2-opcache php7.2-readline ssl-cert
0 upgraded, 42 newly installed, 0 to remove and 18 not upgraded.
Need to get 25.5 MB of archives.
After this operation, 180 MB of additional disk space will be used.
Do you want to continue? [Y/n] y
Get:1 http://azure.archive.ubuntu.com/ubuntu bionic/main amd64 libapr1 amd64 1.6.3-2 [90.9 kB]
Get:2 http://azure.archive.ubuntu.com/ubuntu bionic/main amd64 libaprutil1 amd64 1.6.1-2 [84.4 kB]
Get:3 http://azure.archive.ubuntu.com/ubuntu bionic/main amd64 libaprutil1-dbd-sqlite3 amd64 1.6.1-2 [10.6 kB]
Get:4 http://azure.archive.ubuntu.com/ubuntu bionic/main amd64 libaprutil1-ldap amd64 1.6.1-2 [8764 B]
Get:5 http://azure.archive.ubuntu.com/ubuntu bionic/main amd64 liblua5.2-0 amd64 5.2.4-1.1build1 [108 kB]
Get:6 http://azure.archive.ubuntu.com/ubuntu bionic-updates/main amd64 apache2-bin amd64 2.4.29-1ubuntu4.20 [1071 kB]
Get:7 http://azure.archive.ubuntu.com/ubuntu bionic-updates/main amd64 apache2-utils amd64 2.4.29-1ubuntu4.20 [84.2 kB]
Get:8 http://azure.archive.ubuntu.com/ubuntu bionic-updates/main amd64 apache2-data all 2.4.29-1ubuntu4.20 [160 kB]
Get:9 http://azure.archive.ubuntu.com/ubuntu bionic-updates/main amd64 apache2 amd64 2.4.29-1ubuntu4.20 [95.1 kB]
Get:10 http://azure.archive.ubuntu.com/ubuntu bionic/main amd64 mysql-common all 5.8+1.0.4 [7308 B]
Get:11 http://azure.archive.ubuntu.com/ubuntu bionic-updates/main amd64 libaio1 amd64 0.3.110-5ubuntu0.1 [6476B]
Get:12 http://azure.archive.ubuntu.com/ubuntu bionic-updates/main amd64 mysql-client-core-5.7 amd64 5.7.36-0ubuntu0.18.04.1 [6638 kB]
Get:13 http://azure.archive.ubuntu.com/ubuntu bionic-updates/main amd64 mysql-client-5.7 amd64 5.7.36-0ubuntu0.18.04.1 [1942 kB]
Get:14 http://azure.archive.ubuntu.com/ubuntu bionic-updates/main amd64 mysql-server-core-5.7 amd64 5.7.36-0ubuntu0.18.04.1 [7426 kB]
Get:15 http://azure.archive.ubuntu.com/ubuntu bionic/main amd64 libevent-core-2.1-6 amd64 2.1.8-stable-4build1[85.9 kB]
Get:16 http://azure.archive.ubuntu.com/ubuntu bionic-updates/main amd64 mysql-server-5.7 amd64 5.7.36-0ubuntu0.18.04.1 [2906 kB]
Get:17 http://azure.archive.ubuntu.com/ubuntu bionic/main amd64 php-common all 1:60ubuntu1 [12.1 kB]
Get:18 http://azure.archive.ubuntu.com/ubuntu bionic-updates/main amd64 php7.2-common amd64 7.2.24-0ubuntu0.18.04.10 [889 kB]
Get:19 http://azure.archive.ubuntu.com/ubuntu bionic-updates/main amd64 php7.2-json amd64 7.2.24-0ubuntu0.18.04.10 [18.9 kB]
Get:20 http://azure.archive.ubuntu.com/ubuntu bionic-updates/main amd64 php7.2-opcache amd64 7.2.24-0ubuntu0.18.04.10 [165 kB]
Get:21 http://azure.archive.ubuntu.com/ubuntu bionic-updates/main amd64 php7.2-readline amd64 7.2.24-0ubuntu0.18.04.10 [12.2 kB]
Get:22 http://azure.archive.ubuntu.com/ubuntu bionic/main amd64 libsodium23 amd64 1.0.16-2 [143 kB]
Get:23 http://azure.archive.ubuntu.com/ubuntu bionic-updates/main amd64 php7.2-cli amd64 7.2.24-0ubuntu0.18.04.10 [1408 kB]
Get:24 http://azure.archive.ubuntu.com/ubuntu bionic-updates/main amd64 libapache2-mod-php7.2 amd64 7.2.24-0ubuntu0.18.04.10 [1352 kB]
Get:25 http://azure.archive.ubuntu.com/ubuntu bionic/main amd64 libapache2-mod-php all 1:7.2+60ubuntu1 [3212 B]
Get:26 http://azure.archive.ubuntu.com/ubuntu bionic/main amd64 libhtml-tagset-perl all 3.20-3 [12.1 kB]
Get:27 http://azure.archive.ubuntu.com/ubuntu bionic/main amd64 liburi-perl all 1.73-1 [77.2 kB]
Get:28 http://azure.archive.ubuntu.com/ubuntu bionic/main amd64 libhtml-parser-perl amd64 3.72-3build1 [85.9 kB]
Get:29 http://azure.archive.ubuntu.com/ubuntu bionic/main amd64 libcgi-pm-perl all 4.38-1 [185 kB]
Get:30 http://azure.archive.ubuntu.com/ubuntu bionic/main amd64 libfcgi-perl amd64 0.78-2build1 [32.8 kB]
Get:31 http://azure.archive.ubuntu.com/ubuntu bionic/main amd64 libcgi-fast-perl all 1:2.13-1 [9940 B]
Get:32 http://azure.archive.ubuntu.com/ubuntu bionic/main amd64 libencode-locale-perl all 1.05-1 [12.3 kB]
Get:33 http://azure.archive.ubuntu.com/ubuntu bionic/main amd64 libhtml-template-perl all 2.97-1 [59.0 kB]
Get:34 http://azure.archive.ubuntu.com/ubuntu bionic/main amd64 libtimedate-perl all 2.3000-2 [37.5 kB]
Get:35 http://azure.archive.ubuntu.com/ubuntu bionic/main amd64 libhttp-date-perl all 6.02-1 [10.4 kB]
Get:36 http://azure.archive.ubuntu.com/ubuntu bionic/main amd64 libio-html-perl all 1.001-1 [14.9 kB]
Get:37 http://azure.archive.ubuntu.com/ubuntu bionic/main amd64 liblwp-mediatypes-perl all 6.02-1 [21.7 kB]
Get:38 http://azure.archive.ubuntu.com/ubuntu bionic/main amd64 libhttp-message-perl all 6.14-1 [72.1 kB]
Get:39 http://azure.archive.ubuntu.com/ubuntu bionic-updates/main amd64 mysql-server all 5.7.36-0ubuntu0.18.04.1 [9944 B]
Get:40 http://azure.archive.ubuntu.com/ubuntu bionic-updates/main amd64 php7.2-mysql amd64 7.2.24-0ubuntu0.18.04.10 [117 kB]
Get:41 http://azure.archive.ubuntu.com/ubuntu bionic/main amd64 php-mysql all 1:7.2+60ubuntu1 [2004 B]
Get:42 http://azure.archive.ubuntu.com/ubuntu bionic/main amd64 ssl-cert all 1.0.39 [17.0 kB]
Fetched 25.5 MB in 1s (50.3 MB/s)
Extracting templates from packages: 100%
Preconfiguring packages ...
Selecting previously unselected package libapr1:amd64.
(Reading database ... 76990 files and directories currently installed.)
Preparing to unpack .../00-libapr1_1.6.3-2_amd64.deb ...
Unpacking libapr1:amd64 (1.6.3-2) ...
Selecting previously unselected package libaprutil1:amd64.
Preparing to unpack .../01-libaprutil1_1.6.1-2_amd64.deb ...
Unpacking libaprutil1:amd64 (1.6.1-2) ...
Selecting previously unselected package libaprutil1-dbd-sqlite3:amd64.
Preparing to unpack .../02-libaprutil1-dbd-sqlite3_1.6.1-2_amd64.deb ...
Unpacking libaprutil1-dbd-sqlite3:amd64 (1.6.1-2) ...
Selecting previously unselected package libaprutil1-ldap:amd64.
Preparing to unpack .../03-libaprutil1-ldap_1.6.1-2_amd64.deb ...
Unpacking libaprutil1-ldap:amd64 (1.6.1-2) ...
Selecting previously unselected package liblua5.2-0:amd64.
Preparing to unpack .../04-liblua5.2-0_5.2.4-1.1build1_amd64.deb ...
Unpacking liblua5.2-0:amd64 (5.2.4-1.1build1) ...
Selecting previously unselected package apache2-bin.
Preparing to unpack .../05-apache2-bin_2.4.29-1ubuntu4.20_amd64.deb ...
Unpacking apache2-bin (2.4.29-1ubuntu4.20) ...
Selecting previously unselected package apache2-utils.
Preparing to unpack .../06-apache2-utils_2.4.29-1ubuntu4.20_amd64.deb ...
Unpacking apache2-utils (2.4.29-1ubuntu4.20) ...
Selecting previously unselected package apache2-data.
Preparing to unpack .../07-apache2-data_2.4.29-1ubuntu4.20_all.deb ...
Unpacking apache2-data (2.4.29-1ubuntu4.20) ...
Selecting previously unselected package apache2.
Preparing to unpack .../08-apache2_2.4.29-1ubuntu4.20_amd64.deb ...
Unpacking apache2 (2.4.29-1ubuntu4.20) ...
Selecting previously unselected package mysql-common.
Preparing to unpack .../09-mysql-common_5.8+1.0.4_all.deb ...
Unpacking mysql-common (5.8+1.0.4) ...
Selecting previously unselected package libaio1:amd64.
Preparing to unpack .../10-libaio1_0.3.110-5ubuntu0.1_amd64.deb ...
Unpacking libaio1:amd64 (0.3.110-5ubuntu0.1) ...
Selecting previously unselected package mysql-client-core-5.7.
Preparing to unpack .../11-mysql-client-core-5.7_5.7.36-0ubuntu0.18.04.1_amd64.deb ...
Unpacking mysql-client-core-5.7 (5.7.36-0ubuntu0.18.04.1) ...
Selecting previously unselected package mysql-client-5.7.
Preparing to unpack .../12-mysql-client-5.7_5.7.36-0ubuntu0.18.04.1_amd64.deb ...
Unpacking mysql-client-5.7 (5.7.36-0ubuntu0.18.04.1) ...
Selecting previously unselected package mysql-server-core-5.7.
Preparing to unpack .../13-mysql-server-core-5.7_5.7.36-0ubuntu0.18.04.1_amd64.deb ...
Unpacking mysql-server-core-5.7 (5.7.36-0ubuntu0.18.04.1) ...
Selecting previously unselected package libevent-core-2.1-6:amd64.
Preparing to unpack .../14-libevent-core-2.1-6_2.1.8-stable-4build1_amd64.deb ...
Unpacking libevent-core-2.1-6:amd64 (2.1.8-stable-4build1) ...
Setting up mysql-common (5.8+1.0.4) ...
update-alternatives: using /etc/mysql/my.cnf.fallback to provide /etc/mysql/my.cnf (my.cnf) in auto mode
Selecting previously unselected package mysql-server-5.7.
(Reading database ... 77864 files and directories currently installed.)
Preparing to unpack .../00-mysql-server-5.7_5.7.36-0ubuntu0.18.04.1_amd64.deb ...
Unpacking mysql-server-5.7 (5.7.36-0ubuntu0.18.04.1) ...
Selecting previously unselected package php-common.
Preparing to unpack .../01-php-common_1%3a60ubuntu1_all.deb ...
Unpacking php-common (1:60ubuntu1) ...
Selecting previously unselected package php7.2-common.
Preparing to unpack .../02-php7.2-common_7.2.24-0ubuntu0.18.04.10_amd64.deb ...
Unpacking php7.2-common (7.2.24-0ubuntu0.18.04.10) ...
Selecting previously unselected package php7.2-json.
Preparing to unpack .../03-php7.2-json_7.2.24-0ubuntu0.18.04.10_amd64.deb ...
Unpacking php7.2-json (7.2.24-0ubuntu0.18.04.10) ...
Selecting previously unselected package php7.2-opcache.
Preparing to unpack .../04-php7.2-opcache_7.2.24-0ubuntu0.18.04.10_amd64.deb ...
Unpacking php7.2-opcache (7.2.24-0ubuntu0.18.04.10) ...
Selecting previously unselected package php7.2-readline.
Preparing to unpack .../05-php7.2-readline_7.2.24-0ubuntu0.18.04.10_amd64.deb ...
Unpacking php7.2-readline (7.2.24-0ubuntu0.18.04.10) ...
Selecting previously unselected package libsodium23:amd64.
Preparing to unpack .../06-libsodium23_1.0.16-2_amd64.deb ...
Unpacking libsodium23:amd64 (1.0.16-2) ...
Selecting previously unselected package php7.2-cli.
Preparing to unpack .../07-php7.2-cli_7.2.24-0ubuntu0.18.04.10_amd64.deb ...
Unpacking php7.2-cli (7.2.24-0ubuntu0.18.04.10) ...
Selecting previously unselected package libapache2-mod-php7.2.
Preparing to unpack .../08-libapache2-mod-php7.2_7.2.24-0ubuntu0.18.04.10_amd64.deb ...
Unpacking libapache2-mod-php7.2 (7.2.24-0ubuntu0.18.04.10) ...
Selecting previously unselected package libapache2-mod-php.
Preparing to unpack .../09-libapache2-mod-php_1%3a7.2+60ubuntu1_all.deb ...
Unpacking libapache2-mod-php (1:7.2+60ubuntu1) ...
Selecting previously unselected package libhtml-tagset-perl.
Preparing to unpack .../10-libhtml-tagset-perl_3.20-3_all.deb ...
Unpacking libhtml-tagset-perl (3.20-3) ...
Selecting previously unselected package liburi-perl.
Preparing to unpack .../11-liburi-perl_1.73-1_all.deb ...
Unpacking liburi-perl (1.73-1) ...
Selecting previously unselected package libhtml-parser-perl.
Preparing to unpack .../12-libhtml-parser-perl_3.72-3build1_amd64.deb ...
Unpacking libhtml-parser-perl (3.72-3build1) ...
Selecting previously unselected package libcgi-pm-perl.
Preparing to unpack .../13-libcgi-pm-perl_4.38-1_all.deb ...
Unpacking libcgi-pm-perl (4.38-1) ...
Selecting previously unselected package libfcgi-perl.
Preparing to unpack .../14-libfcgi-perl_0.78-2build1_amd64.deb ...
Unpacking libfcgi-perl (0.78-2build1) ...
Selecting previously unselected package libcgi-fast-perl.
Preparing to unpack .../15-libcgi-fast-perl_1%3a2.13-1_all.deb ...
Unpacking libcgi-fast-perl (1:2.13-1) ...
Selecting previously unselected package libencode-locale-perl.
Preparing to unpack .../16-libencode-locale-perl_1.05-1_all.deb ...
Unpacking libencode-locale-perl (1.05-1) ...
Selecting previously unselected package libhtml-template-perl.
Preparing to unpack .../17-libhtml-template-perl_2.97-1_all.deb ...
Unpacking libhtml-template-perl (2.97-1) ...
Selecting previously unselected package libtimedate-perl.
Preparing to unpack .../18-libtimedate-perl_2.3000-2_all.deb ...
Unpacking libtimedate-perl (2.3000-2) ...
Selecting previously unselected package libhttp-date-perl.
Preparing to unpack .../19-libhttp-date-perl_6.02-1_all.deb ...
Unpacking libhttp-date-perl (6.02-1) ...
Selecting previously unselected package libio-html-perl.
Preparing to unpack .../20-libio-html-perl_1.001-1_all.deb ...
Unpacking libio-html-perl (1.001-1) ...
Selecting previously unselected package liblwp-mediatypes-perl.
Preparing to unpack .../21-liblwp-mediatypes-perl_6.02-1_all.deb ...
Unpacking liblwp-mediatypes-perl (6.02-1) ...
Selecting previously unselected package libhttp-message-perl.
Preparing to unpack .../22-libhttp-message-perl_6.14-1_all.deb ...
Unpacking libhttp-message-perl (6.14-1) ...
Selecting previously unselected package mysql-server.
Preparing to unpack .../23-mysql-server_5.7.36-0ubuntu0.18.04.1_all.deb ...
Unpacking mysql-server (5.7.36-0ubuntu0.18.04.1) ...
Selecting previously unselected package php7.2-mysql.
Preparing to unpack .../24-php7.2-mysql_7.2.24-0ubuntu0.18.04.10_amd64.deb ...
Unpacking php7.2-mysql (7.2.24-0ubuntu0.18.04.10) ...
Selecting previously unselected package php-mysql.
Preparing to unpack .../25-php-mysql_1%3a7.2+60ubuntu1_all.deb ...
Unpacking php-mysql (1:7.2+60ubuntu1) ...
Selecting previously unselected package ssl-cert.
Preparing to unpack .../26-ssl-cert_1.0.39_all.deb ...
Unpacking ssl-cert (1.0.39) ...
Setting up libhtml-tagset-perl (3.20-3) ...
Setting up libapr1:amd64 (1.6.3-2) ...
Setting up libevent-core-2.1-6:amd64 (2.1.8-stable-4build1) ...
Setting up libencode-locale-perl (1.05-1) ...
Setting up libtimedate-perl (2.3000-2) ...
Setting up libio-html-perl (1.001-1) ...
Setting up apache2-data (2.4.29-1ubuntu4.20) ...
Setting up ssl-cert (1.0.39) ...
Setting up libsodium23:amd64 (1.0.16-2) ...
Setting up liblwp-mediatypes-perl (6.02-1) ...
Setting up libaio1:amd64 (0.3.110-5ubuntu0.1) ...
Setting up liburi-perl (1.73-1) ...
Setting up libaprutil1:amd64 (1.6.1-2) ...
Setting up php-common (1:60ubuntu1) ...
Created symlink /etc/systemd/system/timers.target.wants/phpsessionclean.timer → /lib/systemd/system/phpsessionclean.timer.
Setting up libhtml-parser-perl (3.72-3build1) ...
Setting up libcgi-pm-perl (4.38-1) ...
Setting up liblua5.2-0:amd64 (5.2.4-1.1build1) ...
Setting up mysql-client-core-5.7 (5.7.36-0ubuntu0.18.04.1) ...
Setting up libfcgi-perl (0.78-2build1) ...
Setting up libaprutil1-ldap:amd64 (1.6.1-2) ...
Setting up libhttp-date-perl (6.02-1) ...
Setting up php7.2-common (7.2.24-0ubuntu0.18.04.10) ...

Creating config file /etc/php/7.2/mods-available/calendar.ini with new version

Creating config file /etc/php/7.2/mods-available/ctype.ini with new version

Creating config file /etc/php/7.2/mods-available/exif.ini with new version

Creating config file /etc/php/7.2/mods-available/fileinfo.ini with new version

Creating config file /etc/php/7.2/mods-available/ftp.ini with new version

Creating config file /etc/php/7.2/mods-available/gettext.ini with new version

Creating config file /etc/php/7.2/mods-available/iconv.ini with new version

Creating config file /etc/php/7.2/mods-available/pdo.ini with new version

Creating config file /etc/php/7.2/mods-available/phar.ini with new version

Creating config file /etc/php/7.2/mods-available/posix.ini with new version

Creating config file /etc/php/7.2/mods-available/shmop.ini with new version

Creating config file /etc/php/7.2/mods-available/sockets.ini with new version

Creating config file /etc/php/7.2/mods-available/sysvmsg.ini with new version

Creating config file /etc/php/7.2/mods-available/sysvsem.ini with new version

Creating config file /etc/php/7.2/mods-available/sysvshm.ini with new version

Creating config file /etc/php/7.2/mods-available/tokenizer.ini with new version
Setting up libhtml-template-perl (2.97-1) ...
Setting up libaprutil1-dbd-sqlite3:amd64 (1.6.1-2) ...
Setting up mysql-server-core-5.7 (5.7.36-0ubuntu0.18.04.1) ...
Setting up apache2-utils (2.4.29-1ubuntu4.20) ...
Setting up apache2-bin (2.4.29-1ubuntu4.20) ...
Setting up libcgi-fast-perl (1:2.13-1) ...
Setting up php7.2-readline (7.2.24-0ubuntu0.18.04.10) ...

Creating config file /etc/php/7.2/mods-available/readline.ini with new version
Setting up libhttp-message-perl (6.14-1) ...
Setting up php7.2-json (7.2.24-0ubuntu0.18.04.10) ...

Creating config file /etc/php/7.2/mods-available/json.ini with new version
Setting up mysql-client-5.7 (5.7.36-0ubuntu0.18.04.1) ...
Setting up php7.2-opcache (7.2.24-0ubuntu0.18.04.10) ...

Creating config file /etc/php/7.2/mods-available/opcache.ini with new version
Setting up php7.2-mysql (7.2.24-0ubuntu0.18.04.10) ...

Creating config file /etc/php/7.2/mods-available/mysqlnd.ini with new version

Creating config file /etc/php/7.2/mods-available/mysqli.ini with new version

Creating config file /etc/php/7.2/mods-available/pdo_mysql.ini with new version
Setting up apache2 (2.4.29-1ubuntu4.20) ...
Enabling module mpm_event.
Enabling module authz_core.
Enabling module authz_host.
Enabling module authn_core.
Enabling module auth_basic.
Enabling module access_compat.
Enabling module authn_file.
Enabling module authz_user.
Enabling module alias.
Enabling module dir.
Enabling module autoindex.
Enabling module env.
Enabling module mime.
Enabling module negotiation.
Enabling module setenvif.
Enabling module filter.
Enabling module deflate.
Enabling module status.
Enabling module reqtimeout.
Enabling conf charset.
Enabling conf localized-error-pages.
Enabling conf other-vhosts-access-log.
Enabling conf security.
Enabling conf serve-cgi-bin.
Enabling site 000-default.
Created symlink /etc/systemd/system/multi-user.target.wants/apache2.service → /lib/systemd/system/apache2.service.
Created symlink /etc/systemd/system/multi-user.target.wants/apache-htcacheclean.service → /lib/systemd/system/apache-htcacheclean.service.
Setting up php7.2-cli (7.2.24-0ubuntu0.18.04.10) ...
update-alternatives: using /usr/bin/php7.2 to provide /usr/bin/php (php) in auto mode
update-alternatives: using /usr/bin/phar7.2 to provide /usr/bin/phar (phar) in auto mode
update-alternatives: using /usr/bin/phar.phar7.2 to provide /usr/bin/phar.phar (phar.phar) in auto mode

Creating config file /etc/php/7.2/cli/php.ini with new version
Setting up mysql-server-5.7 (5.7.36-0ubuntu0.18.04.1) ...
update-alternatives: using /etc/mysql/mysql.cnf to provide /etc/mysql/my.cnf (my.cnf) in auto mode
Renaming removed key_buffer and myisam-recover options (if present)
Created symlink /etc/systemd/system/multi-user.target.wants/mysql.service → /lib/systemd/system/mysql.service.
Setting up libapache2-mod-php7.2 (7.2.24-0ubuntu0.18.04.10) ...

Creating config file /etc/php/7.2/apache2/php.ini with new version
Module mpm_event disabled.
Enabling module mpm_prefork.
apache2_switch_mpm Switch to prefork
apache2_invoke: Enable module php7.2
Setting up php-mysql (1:7.2+60ubuntu1) ...
Setting up mysql-server (5.7.36-0ubuntu0.18.04.1) ...
Setting up libapache2-mod-php (1:7.2+60ubuntu1) ...
Processing triggers for libc-bin (2.27-3ubuntu1.4) ...
Processing triggers for systemd (237-3ubuntu10.52) ...
Processing triggers for man-db (2.8.3-2ubuntu0.1) ...
Processing triggers for ufw (0.36-0ubuntu0.18.04.2) ...
Processing triggers for ureadahead (0.100.0-21) ...
```
**Verify Apache**
command to verify Apache
```
apache2 -v
```
```
Output

Server version: Apache/2.4.29 (Ubuntu)
Server built:   2021-11-14T23:52:18
```
![Apache2 Ubuntu](https://user-images.githubusercontent.com/94197561/147291837-20beea9f-d072-4056-aa44-e6c19d80baad.png)


## 6. Installing WordPress
**command for installing wordpress**
```
sudo apt install wordpress
```
```
Output

Reading package lists... Done
Building dependency tree
Reading state information... Done
The following package was automatically installed and is no longer required:
  linux-headers-4.15.0-163
Use 'sudo apt autoremove' to remove it.
The following additional packages will be installed:
  fontconfig-config fonts-dejavu-core javascript-common libao-common libao4 libflac8 libfontconfig1 libgd3
  libjbig0 libjpeg-turbo8 libjpeg8 libjs-cropper libjs-prototype libjs-scriptaculous libogg0 libphp-phpmailer
  libspeex1 libtiff5 libvorbis0a libvorbisenc2 libvorbisfile3 libwebp6 libxpm4 php-gd php-getid3 php7.2-gd
  vorbis-tools wordpress-l10n wordpress-theme-twentyseventeen
Suggested packages:
  libasound2 libaudio2 libpulse0 libsndio6.1 libgd-tools mail-transport-agent php-league-oauth2-client
  php-league-oauth2-google speex php-ssh2
The following NEW packages will be installed:
  fontconfig-config fonts-dejavu-core javascript-common libao-common libao4 libflac8 libfontconfig1 libgd3
  libjbig0 libjpeg-turbo8 libjpeg8 libjs-cropper libjs-prototype libjs-scriptaculous libogg0 libphp-phpmailer
  libspeex1 libtiff5 libvorbis0a libvorbisenc2 libvorbisfile3 libwebp6 libxpm4 php-gd php-getid3 php7.2-gd
  vorbis-tools wordpress wordpress-l10n wordpress-theme-twentyseventeen
0 upgraded, 30 newly installed, 0 to remove and 18 not upgraded.
Need to get 13.1 MB of archives.
After this operation, 69.0 MB of additional disk space will be used.
Do you want to continue? [Y/n] y
Get:1 http://azure.archive.ubuntu.com/ubuntu bionic-updates/main amd64 libjpeg-turbo8 amd64 1.5.2-0ubuntu5.18.04.4 [110 kB]
Get:2 http://azure.archive.ubuntu.com/ubuntu bionic/main amd64 libogg0 amd64 1.3.2-1 [17.2 kB]
Get:3 http://azure.archive.ubuntu.com/ubuntu bionic/main amd64 fonts-dejavu-core all 2.37-1 [1041 kB]
Get:4 http://azure.archive.ubuntu.com/ubuntu bionic/main amd64 fontconfig-config all 2.12.6-0ubuntu2 [55.8 kB]
Get:5 http://azure.archive.ubuntu.com/ubuntu bionic/main amd64 javascript-common all 11 [6066 B]
Get:6 http://azure.archive.ubuntu.com/ubuntu bionic/main amd64 libao-common all 1.2.2+20180113-1ubuntu1 [6644 B]
Get:7 http://azure.archive.ubuntu.com/ubuntu bionic/main amd64 libao4 amd64 1.2.2+20180113-1ubuntu1 [35.1 kB]
Get:8 http://azure.archive.ubuntu.com/ubuntu bionic/main amd64 libflac8 amd64 1.3.2-1 [213 kB]
Get:9 http://azure.archive.ubuntu.com/ubuntu bionic/main amd64 libfontconfig1 amd64 2.12.6-0ubuntu2 [137 kB]
Get:10 http://azure.archive.ubuntu.com/ubuntu bionic/main amd64 libjpeg8 amd64 8c-2ubuntu8 [2194 B]
Get:11 http://azure.archive.ubuntu.com/ubuntu bionic/main amd64 libjbig0 amd64 2.1-3.1build1 [26.7 kB]
Get:12 http://azure.archive.ubuntu.com/ubuntu bionic-updates/main amd64 libtiff5 amd64 4.0.9-5ubuntu0.4 [153 kB]
Get:13 http://azure.archive.ubuntu.com/ubuntu bionic-updates/main amd64 libwebp6 amd64 0.6.1-2ubuntu0.18.04.1 [186 kB]
Get:14 http://azure.archive.ubuntu.com/ubuntu bionic/main amd64 libxpm4 amd64 1:3.5.12-1 [34.0 kB]
Get:15 http://azure.archive.ubuntu.com/ubuntu bionic-updates/main amd64 libgd3 amd64 2.2.5-4ubuntu0.5 [119 kB]
Get:16 http://azure.archive.ubuntu.com/ubuntu bionic/universe amd64 libjs-prototype all 1.7.1-3 [44.2 kB]
Get:17 http://azure.archive.ubuntu.com/ubuntu bionic/universe amd64 libjs-scriptaculous all 1.9.0-2 [107 kB]
Get:18 http://azure.archive.ubuntu.com/ubuntu bionic/universe amd64 libjs-cropper all 1.2.2-1 [139 kB]
Get:19 http://azure.archive.ubuntu.com/ubuntu bionic-updates/universe amd64 libphp-phpmailer all 5.2.14+dfsg-2.3+deb9u2build0.18.04.1 [135 kB]
Get:20 http://azure.archive.ubuntu.com/ubuntu bionic/main amd64 libspeex1 amd64 1.2~rc1.2-1ubuntu2 [52.1 kB]
Get:21 http://azure.archive.ubuntu.com/ubuntu bionic/main amd64 libvorbis0a amd64 1.3.5-4.2 [86.4 kB]
Get:22 http://azure.archive.ubuntu.com/ubuntu bionic/main amd64 libvorbisenc2 amd64 1.3.5-4.2 [70.7 kB]
Get:23 http://azure.archive.ubuntu.com/ubuntu bionic/main amd64 libvorbisfile3 amd64 1.3.5-4.2 [16.0 kB]
Get:24 http://azure.archive.ubuntu.com/ubuntu bionic-updates/main amd64 php7.2-gd amd64 7.2.24-0ubuntu0.18.04.10 [27.1 kB]
Get:25 http://azure.archive.ubuntu.com/ubuntu bionic/main amd64 php-gd all 1:7.2+60ubuntu1 [1996 B]
Get:26 http://azure.archive.ubuntu.com/ubuntu bionic/universe amd64 php-getid3 all 1.9.15+dfsg-1 [339 kB]
Get:27 http://azure.archive.ubuntu.com/ubuntu bionic/universe amd64 vorbis-tools amd64 1.4.0-10.1 [183 kB]
Get:28 http://azure.archive.ubuntu.com/ubuntu bionic/universe amd64 wordpress all 4.9.5+dfsg1-1 [4472 kB]
Get:29 http://azure.archive.ubuntu.com/ubuntu bionic/universe amd64 wordpress-l10n all 4.9.5+dfsg1-1 [4365 kB]
Get:30 http://azure.archive.ubuntu.com/ubuntu bionic/universe amd64 wordpress-theme-twentyseventeen all 4.9.5+dfsg1-1 [891 kB]
Fetched 13.1 MB in 0s (56.4 MB/s)
Selecting previously unselected package libjpeg-turbo8:amd64.
(Reading database ... 78389 files and directories currently installed.)
Preparing to unpack .../00-libjpeg-turbo8_1.5.2-0ubuntu5.18.04.4_amd64.deb ...
Unpacking libjpeg-turbo8:amd64 (1.5.2-0ubuntu5.18.04.4) ...
Selecting previously unselected package libogg0:amd64.
Preparing to unpack .../01-libogg0_1.3.2-1_amd64.deb ...
Unpacking libogg0:amd64 (1.3.2-1) ...
Selecting previously unselected package fonts-dejavu-core.
Preparing to unpack .../02-fonts-dejavu-core_2.37-1_all.deb ...
Unpacking fonts-dejavu-core (2.37-1) ...
Selecting previously unselected package fontconfig-config.
Preparing to unpack .../03-fontconfig-config_2.12.6-0ubuntu2_all.deb ...
Unpacking fontconfig-config (2.12.6-0ubuntu2) ...
Selecting previously unselected package javascript-common.
Preparing to unpack .../04-javascript-common_11_all.deb ...
Unpacking javascript-common (11) ...
Selecting previously unselected package libao-common.
Preparing to unpack .../05-libao-common_1.2.2+20180113-1ubuntu1_all.deb ...
Unpacking libao-common (1.2.2+20180113-1ubuntu1) ...
Selecting previously unselected package libao4:amd64.
Preparing to unpack .../06-libao4_1.2.2+20180113-1ubuntu1_amd64.deb ...
Unpacking libao4:amd64 (1.2.2+20180113-1ubuntu1) ...
Selecting previously unselected package libflac8:amd64.
Preparing to unpack .../07-libflac8_1.3.2-1_amd64.deb ...
Unpacking libflac8:amd64 (1.3.2-1) ...
Selecting previously unselected package libfontconfig1:amd64.
Preparing to unpack .../08-libfontconfig1_2.12.6-0ubuntu2_amd64.deb ...
Unpacking libfontconfig1:amd64 (2.12.6-0ubuntu2) ...
Selecting previously unselected package libjpeg8:amd64.
Preparing to unpack .../09-libjpeg8_8c-2ubuntu8_amd64.deb ...
Unpacking libjpeg8:amd64 (8c-2ubuntu8) ...
Selecting previously unselected package libjbig0:amd64.
Preparing to unpack .../10-libjbig0_2.1-3.1build1_amd64.deb ...
Unpacking libjbig0:amd64 (2.1-3.1build1) ...
Selecting previously unselected package libtiff5:amd64.
Preparing to unpack .../11-libtiff5_4.0.9-5ubuntu0.4_amd64.deb ...
Unpacking libtiff5:amd64 (4.0.9-5ubuntu0.4) ...
Selecting previously unselected package libwebp6:amd64.
Preparing to unpack .../12-libwebp6_0.6.1-2ubuntu0.18.04.1_amd64.deb ...
Unpacking libwebp6:amd64 (0.6.1-2ubuntu0.18.04.1) ...
Selecting previously unselected package libxpm4:amd64.
Preparing to unpack .../13-libxpm4_1%3a3.5.12-1_amd64.deb ...
Unpacking libxpm4:amd64 (1:3.5.12-1) ...
Selecting previously unselected package libgd3:amd64.
Preparing to unpack .../14-libgd3_2.2.5-4ubuntu0.5_amd64.deb ...
Unpacking libgd3:amd64 (2.2.5-4ubuntu0.5) ...
Selecting previously unselected package libjs-prototype.
Preparing to unpack .../15-libjs-prototype_1.7.1-3_all.deb ...
Unpacking libjs-prototype (1.7.1-3) ...
Selecting previously unselected package libjs-scriptaculous.
Preparing to unpack .../16-libjs-scriptaculous_1.9.0-2_all.deb ...
Unpacking libjs-scriptaculous (1.9.0-2) ...
Selecting previously unselected package libjs-cropper.
Preparing to unpack .../17-libjs-cropper_1.2.2-1_all.deb ...
Unpacking libjs-cropper (1.2.2-1) ...
Selecting previously unselected package libphp-phpmailer.
Preparing to unpack .../18-libphp-phpmailer_5.2.14+dfsg-2.3+deb9u2build0.18.04.1_all.deb ...
Unpacking libphp-phpmailer (5.2.14+dfsg-2.3+deb9u2build0.18.04.1) ...
Selecting previously unselected package libspeex1:amd64.
Preparing to unpack .../19-libspeex1_1.2~rc1.2-1ubuntu2_amd64.deb ...
Unpacking libspeex1:amd64 (1.2~rc1.2-1ubuntu2) ...
Selecting previously unselected package libvorbis0a:amd64.
Preparing to unpack .../20-libvorbis0a_1.3.5-4.2_amd64.deb ...
Unpacking libvorbis0a:amd64 (1.3.5-4.2) ...
Selecting previously unselected package libvorbisenc2:amd64.
Preparing to unpack .../21-libvorbisenc2_1.3.5-4.2_amd64.deb ...
Unpacking libvorbisenc2:amd64 (1.3.5-4.2) ...
Selecting previously unselected package libvorbisfile3:amd64.
Preparing to unpack .../22-libvorbisfile3_1.3.5-4.2_amd64.deb ...
Unpacking libvorbisfile3:amd64 (1.3.5-4.2) ...
Selecting previously unselected package php7.2-gd.
Preparing to unpack .../23-php7.2-gd_7.2.24-0ubuntu0.18.04.10_amd64.deb ...
Unpacking php7.2-gd (7.2.24-0ubuntu0.18.04.10) ...
Selecting previously unselected package php-gd.
Preparing to unpack .../24-php-gd_1%3a7.2+60ubuntu1_all.deb ...
Unpacking php-gd (1:7.2+60ubuntu1) ...
Selecting previously unselected package php-getid3.
Preparing to unpack .../25-php-getid3_1.9.15+dfsg-1_all.deb ...
Unpacking php-getid3 (1.9.15+dfsg-1) ...
Selecting previously unselected package vorbis-tools.
Preparing to unpack .../26-vorbis-tools_1.4.0-10.1_amd64.deb ...
Unpacking vorbis-tools (1.4.0-10.1) ...
Selecting previously unselected package wordpress.
Preparing to unpack .../27-wordpress_4.9.5+dfsg1-1_all.deb ...
Unpacking wordpress (4.9.5+dfsg1-1) ...
Selecting previously unselected package wordpress-l10n.
Preparing to unpack .../28-wordpress-l10n_4.9.5+dfsg1-1_all.deb ...
Unpacking wordpress-l10n (4.9.5+dfsg1-1) ...
Selecting previously unselected package wordpress-theme-twentyseventeen.
Preparing to unpack .../29-wordpress-theme-twentyseventeen_4.9.5+dfsg1-1_all.deb ...
Unpacking wordpress-theme-twentyseventeen (4.9.5+dfsg1-1) ...
Setting up php-getid3 (1.9.15+dfsg-1) ...
Setting up libjbig0:amd64 (2.1-3.1build1) ...
Setting up fonts-dejavu-core (2.37-1) ...
Setting up wordpress-theme-twentyseventeen (4.9.5+dfsg1-1) ...
Setting up libao-common (1.2.2+20180113-1ubuntu1) ...
Setting up libjpeg-turbo8:amd64 (1.5.2-0ubuntu5.18.04.4) ...
Setting up libspeex1:amd64 (1.2~rc1.2-1ubuntu2) ...
Setting up libogg0:amd64 (1.3.2-1) ...
Setting up libphp-phpmailer (5.2.14+dfsg-2.3+deb9u2build0.18.04.1) ...
Setting up libxpm4:amd64 (1:3.5.12-1) ...
Setting up javascript-common (11) ...
apache2_invoke: Enable configuration javascript-common
Setting up libjs-prototype (1.7.1-3) ...
Setting up libvorbis0a:amd64 (1.3.5-4.2) ...
Setting up libwebp6:amd64 (0.6.1-2ubuntu0.18.04.1) ...
Setting up libjpeg8:amd64 (8c-2ubuntu8) ...
Setting up libvorbisfile3:amd64 (1.3.5-4.2) ...
Setting up fontconfig-config (2.12.6-0ubuntu2) ...
Setting up libao4:amd64 (1.2.2+20180113-1ubuntu1) ...
Setting up libflac8:amd64 (1.3.2-1) ...
Setting up libtiff5:amd64 (4.0.9-5ubuntu0.4) ...
Setting up libjs-scriptaculous (1.9.0-2) ...
Setting up libjs-cropper (1.2.2-1) ...
Setting up libvorbisenc2:amd64 (1.3.5-4.2) ...
Setting up libfontconfig1:amd64 (2.12.6-0ubuntu2) ...
Setting up libgd3:amd64 (2.2.5-4ubuntu0.5) ...
Setting up vorbis-tools (1.4.0-10.1) ...
Setting up php7.2-gd (7.2.24-0ubuntu0.18.04.10) ...

Creating config file /etc/php/7.2/mods-available/gd.ini with new version
Setting up wordpress (4.9.5+dfsg1-1) ...
Added to /var/lib/wordpress/wp-content/plugins: akismet index.php
Added to /var/lib/wordpress/wp-content/languages: admin-ar.mo admin-bs_BA.mo admin-ca.mo admin-cy.mo admin-da_DK.mo admin-de_DE.mo admin-el.mo admin-es_ES.mo admin-es_PE.mo admin-et.mo admin-eu.mo admin-fa_IR.mo admin-fi.mo admin-fr_FR.mo admin-gl_ES.mo admin-he_IL.mo admin-hr.mo admin-it_IT.mo admin-ja.mo admin-ka_GE.mo admin-ko_KR.mo admin-my_MM.mo admin-network-ar.mo admin-network-bs_BA.mo admin-network-ca.mo admin-network-cy.mo admin-network-da_DK.mo admin-network-de_DE.mo admin-network-el.mo admin-network-es_ES.mo admin-network-es_PE.mo admin-network-et.mo admin-network-fa_IR.mo admin-network-fi.mo admin-network-fr_FR.mo admin-network-gl_ES.mo admin-network-he_IL.mo admin-network-hr.mo admin-network-it_IT.mo admin-network-ja.mo admin-network-ka_GE.mo admin-network-ko_KR.mo admin-network-my_MM.mo admin-network-ru_RU.mo admin-network-sk_SK.mo admin-network-sl_SI.mo admin-network-sq.mo admin-network-sr_RS.mo admin-network-sv_SE.mo admin-network-ug_CN.mo admin-network-zh_CN.mo admin-network-zh_TW.mo admin-ru_RU.mo admin-sk_SK.mo admin-sl_SI.mo admin-sq.mo admin-sr_RS.mo admin-sv_SE.mo admin-ug_CN.mo admin-zh_CN.mo admin-zh_TW.mo ar.mo bg_BG.mo bn_BD.mo bs_BA.mo ca.mo ckb.mo continents-cities-bg_BG.mocontinents-cities-bs_BA.mo continents-cities-cs_CZ.mo continents-cities-cy.mo continents-cities-da_DK.mo continents-cities-de_DE.mo continents-cities-el.mo continents-cities-en_CA.mo continents-cities-es_PE.mo continents-cities-et.mo continents-cities-eu.mo continents-cities-fa_IR.mo continents-cities-fi.mo continents-cities-fr_FR.mo continents-cities-gd.mo continents-cities-he_IL.mo continents-cities-hr.mo continents-cities-hu_HU.mo continents-cities-it_IT.mo continents-cities-ja.mo continents-cities-ka_GE.mo continents-cities-ko_KR.mo continents-cities-lv.mo continents-cities-mk_MK.mo continents-cities-my_MM.mo continents-cities-nb_NO.mo continents-cities-nn_NO.mo continents-cities-pl_PL.mo continents-cities-pt_BR.mo continents-cities-pt_PT.mo continents-cities-ro_RO.mo continents-cities-ru_RU.mo continents-cities-sk_SK.mo continents-cities-sl_SI.mo continents-cities-sq.mocontinents-cities-sr_RS.mo continents-cities-su_ID.mo continents-cities-sv_SE.mo continents-cities-ta_LK.mo continents-cities-tr_TR.mo continents-cities-ug_CN.mo continents-cities-vi.mo continents-cities-zh_CN.mo continents-cities-zh_TW.mo cs_CZ.mo cy.mo da_DK.mo de_DE.mo el.mo en_CA.mo eo.mo es_CL.mo es_ES.mo es_PE.mo et.mo eu.mofa_IR.mo fi.mo fr_FR.mo gd.mo gl_ES.mo he_IL.mo hr.mo hu_HU.mo id_ID.mo it_IT.mo ja.mo jv_ID.mo ka_GE.mo ko_KR.mo lv.mo mk_MK.mo ms_MY.mo my_MM.mo nb_NO.mo nl.mo nl_NL.mo pl_PL.mo pt_BR.mo pt_PT.mo ro_RO.mo ru_RU.mo ru_UA.mo si_LK.mo sk_SK.mo sl_SI.mo sq.mo sr_RS.mo su_ID.mo sv_SE.mo sw.mo ta_LK.mo th.mo tr_TR.mo ug_CN.mo uk.mo ur.mo vi.mo zh_CN.mo zh_HK.mo zh_TW.mo
Setting up wordpress-l10n (4.9.5+dfsg1-1) ...
Setting up php-gd (1:7.2+60ubuntu1) ...
Processing triggers for mime-support (3.60ubuntu1) ...
Processing triggers for libc-bin (2.27-3ubuntu1.4) ...
Processing triggers for man-db (2.8.3-2ubuntu0.1) ...
Processing triggers for libapache2-mod-php7.2 (7.2.24-0ubuntu0.18.04.10) ...
```
