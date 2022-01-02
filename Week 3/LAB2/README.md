# Lab 2: Install a LAMP stack on an Azure Linux VM

1. Prepare the LAMP server
2. Test your Lamp server
3. Secure the database server
4. (Optional) Install phpMyAdmin

### Notes:

Tutorial: Install a LAMP web server on the Amazon Linux AMI
* https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/install-LAMP.html

Tutorial: Host a WordPress blog on Amazon Linux 2
* https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/hosting-wordpress.html

Sample Gist
* https://gist.github.com/mikepfeiffer/c079608703e604224e58a3d40d0fa043#file-lamp-linux-aws-sh


# Things learnt whilst Installing a LAMP web server on the Amazon Linux AMI


**1. Prepare the LAMP server**

 To prepare a lamb server the following needs to be done:
 
* Connect to your instance

* perform a quick software update on your instance

* install the LAMP web server

Command for installing a LAMP web server
```
sudo amazon-linux-extras install -y lamp-mariadb10.2-php7.2 php7.2
```
```
**OUTPUT**

Installed:
  mariadb.x86_64 3:10.2.38-1.amzn2.0.1      php-cli.x86_64 0:7.2.34-1.amzn2      php-fpm.x86_64 0:7.2.34-1.amzn2      php-json.x86_64 0:7.2.34-1.amzn2
  php-mysqlnd.x86_64 0:7.2.34-1.amzn2       php-pdo.x86_64 0:7.2.34-1.amzn2
```

After installing the LAMP webserver, I installed the Apache web server, MariaDB, and PHP software packages and then I tested my web server by typing the public IP address of my instance in a web server.

The image below is the result from pasting my public IP address in a web server

![Apache2 Ubuntu](https://user-images.githubusercontent.com/94197561/147888924-53d9e97d-a9a4-4020-83e3-2f91a22367a1.png)


**2. Test the Lamp server**
