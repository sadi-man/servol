---
title: "6 Step Install OpenLiteSpeed, MariaDB, PHP8.0 on Ubuntu 20.04"
description: "Learn how to install OpenLiteSpeed, MariaDB, and PHP8.0 on Ubuntu 20.04 with this easy 6-step guide. Get your web server up and running smoothly!"
date: "2023-07-03"
categories:
- "Openlitespeed"
---

If you're looking to set up a powerful web server environment on your Ubuntu 20.04 system, this guide will walk you through the process of [install OpenLiteSpeed](https://kumiskiri.com/cara-install-openlitespeed-ubuntu/), MariaDB, and PHP8.0. These components will provide you with a reliable and efficient platform to host your websites and applications. Let's get started!

## Install OpenLiteSpeed Ubuntu

A number of steps that you must follow so that the Install OpenLiteSpeed Ubuntu process runs successfully, do it carefully

### Step 1: Updating Software Packages

To ensure that your system has the latest software packages, we need to update them. Run the following command in your terminal:

sudo apt update && sudo apt upgrade -y

### Step 2: Installing OpenLiteSpeed Web Server

OpenLiteSpeed is a high-performance web server that can handle a large number of concurrent connections. To install it, follow these steps:

Adding the OpenLiteSpeed Repository
First, we need to add the OpenLiteSpeed repository to our system. Run the following command:

wget -O - http://rpms.litespeedtech.com/debian/enable_lst_debian_repo.sh | sudo bash

Installing OpenLiteSpeed

Once the repository is added, we can proceed with the installation. Run the following command:

sudo apt install -y openlitespeed

Starting OpenLiteSpeed

To start the OpenLiteSpeed service, run the following commands:

sudo systemctl enable lshttpd
sudo systemctl start lshttpd

Checking the Status

You can verify the status of OpenLiteSpeed by running the following command:

sudo systemctl status lshttpd

Configuring the Listener

Next, we need to configure the listener to use port 80 instead of the default port 8088. Follow these steps:

Open the configuration file in the nano text editor:

sudo nano /usr/local/lsws/conf/httpd_config.conf

Locate the following lines:

listener Default{
    address                  *:8088
    secure                   0
    map                      Example *
}

Change the port number from 8088 to 80:

listener Default{
    address                  *:80
    secure                   0
    map                      Example *
}

Save and close the file by pressing Ctrl + X, followed by Y, and then Enter.

Restart OpenLiteSpeed for the changes to take effect:

sudo systemctl restart lshttpd

### Step 3: Installing MariaDB Database Server

MariaDB is a popular open-source relational database management system. Follow these steps to install it:

sudo apt install mariadb-server mariadb-client

Starting and Enabling MariaDB

To start the MariaDB service and enable it to start on system boot, run the following commands:

sudo systemctl start mariadb
sudo systemctl enable mariadb

Securing MariaDB

To improve the security of your MariaDB installation, you should run the security script and follow the prompts:

sudo mysql_secure_installation

### Step 4: Installing PHP8.0

PHP is a widely used scripting language for web development. Install PHP8.0 along with necessary modules by executing the following command:

sudo apt install lsphp80 lsphp80-mysql lsphp80-common lsphp80-opcache lsphp80-curl

Checking PHP Version

You can check the installed PHP version by running the following command:

/usr/local/lsws/lsphp80/bin/php8.0 -v

Checking Installed PHP Modules

To view the list of installed PHP modules, use the following command:

/usr/local/lsws/lsphp80/bin/php8.0 --modules

### Step 5: Testing PHP

To ensure that PHP is working correctly with OpenLiteSpeed, you can create a test file. Follow these steps:

Create a new file called info.php in the web server's document root directory:

sudo nano /var/www/html/info.php

Add the following line to the file:

<?php phpinfo(); ?>
Save and close the file.

Open your web browser and navigate to http://your_server_ip/info.php. You should see the PHP information page if everything is set up correctly.

### Step 6: Configuring the OpenLiteSpeed Admin Panel

To configure the OpenLiteSpeed admin panel, follow these steps:

Set a username and password for the admin panel by running the following command:

sudo /usr/local/lsws/admin/misc/admpass.sh

Access the admin panel by visiting https://your_server_ip:7080/login.php in your web browser.

Enter the following information:

Name: lsphp8.0
Address: uds://tmp/lshttpd/lsphp80.sock
Max Connections: 10
Environment: PHP_LSAPI_CHILDREN=10
LSAPI_AVOID_FORK=200M
Initial Request Timeout (secs): 60
Retry Timeout (secs): 0
Persistent Connection: Yes
Response Buffering: No
Command: lsphp80/bin/lsphp
Backlog: 100
Instances: 1
Priority: 0
Memory Soft Limit (bytes): 2047M
Memory Hard Limit (bytes): 2047M
Process Soft Limit: 1400
Process Hard Limit: 1500

Save the settings.

Openlistspeed script handler

Suffixes: php
Handler Type: LiteSpeed SAPI
Handler Name: lsphp8.0
openlitespeed script handler php8.0

openlitespeed multiple PHP versions

cat /etc/php/7.4/mods-available/* | sudo tee -a /etc/php/7.4/fpm/php.ini
cat /etc/php/7.4/mods-available/* | sudo tee -a /etc/php/7.4/cli/php.ini

Conclusion

Congratulations! You have successfully installed OpenLiteSpeed, MariaDB, and PHP8.0 on your Ubuntu 20.04 system. This powerful web server stack will enable you to host and serve websites and applications efficiently. Enjoy your optimized web hosting environment!

Source: https://kumiskiri.com/cara-install-openlitespeed-ubuntu/
