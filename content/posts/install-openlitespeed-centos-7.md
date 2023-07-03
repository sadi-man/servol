---
title: "Install OpenLiteSpeed CentOS 7 And Ubuntu: A 11 Step Guide"
description: "Install OpenLiteSpeed on CentOS 7 and Ubuntu with Our 11-Step Guide. Unlock Lightning-Fast Speeds Today!"
date: "2023-06-03"
categories:
- "Openlitespeed"
---

OpenLiteSpeed is a high-performance web server that can greatly enhance the speed and efficiency of your website. In this guide, we will walk you through the process of [installing OpenLiteSpeed](https://kumiskiri.com/cara-install-openlitespeed-ubuntu/) CentOS 7 and Ubuntu. By following these steps, you'll be able to set up and configure OpenLiteSpeed to optimize the performance of your website.

## Install OpenLiteSpeed CentOS 7 And Ubuntu

a number of steps that you must follow so that the openlitespeed installation process runs successfully, do it carefully

### Step 1: Setting up the Repository

To begin the installation process, you need to set up the OpenLiteSpeed repository. Execute the following command to add the repository:

rpm -ivh http://rpms.litespeedtech.com/centos/litespeed-repo-1.1-1.el7.noarch.rpm

### Step 2: Installing Dependencies

Next, you need to install the necessary dependencies for OpenLiteSpeed. Run the following commands:

yum install epel-release
yum install openlitespeed

### Step 3: Installing PHP and Extensions

To enable PHP support, you need to install PHP and its extensions. Use the following command:

yum install lsphp74 lsphp74-json lsphp74-xmlrpc lsphp74-xml lsphp74-tidy lsphp74-soap lsphp74-snmp lsphp74-pspell lsphp74-process lsphp74-pgsql lsphp74-pear lsphp74-pdo lsphp74-opcache lsphp74-odbc lsphp74-mysqlnd lsphp74-mcrypt lsphp74-mbstring lsphp74-ldap lsphp74-intl lsphp74-imap lsphp74-gmp lsphp74-gd lsphp74-enchant lsphp74-dba lsphp74-common lsphp74-bcmath lsphp74-memcached lsphp74-redis

### Step 4: Configuring OpenLiteSpeed for CentOS 7

Now that you have installed OpenLiteSpeed and PHP, it's time to configure them. Follow these steps:

Run the following command to download the necessary script:

wget -O - http://rpms.litespeedtech.com/debian/enable_lst_debian_repo.sh | bash

Install OpenLiteSpeed using the command:

apt install openlitespeed

Install PHP and its extensions by executing the following command:

apt install lsphp74 lsphp74-common lsphp74-curl lsphp74-dev lsphp74-imap lsphp74-intl lsphp74-json lsphp74-ldap lsphp74-mysql lsphp74-opcache lsphp74-pspell lsphp74-memcached lsphp74-redis lsphp74-sqlite3 lsphp74-tidy

### Step 5: Creating User and Directory

To ensure proper ownership and permissions, create a user and directory for your domain. Use the following commands as a guide:

groupadd group-name
useradd -M -g group-name user-name
mkdir /home/domain.com
mkdir /home/domain.com/public_html
chown user-name:group-name /home/domain.com
chmod 711 /home/domain.com
chown user-name:nobody /home/domain.com/public_html
chmod 750 /home/domain.com/public_html

### Step 6: Testing the Configuration

To verify that everything is set up correctly, you can create a test page. Run the following commands:

touch /home/domain.com/public_html/.htaccess
chown -R user-name:group-name /home/domain.com/public_html/.htaccess
echo "<?php phpinfo();" > /home/domain.com/public_html/info.php
echo "hello world" > /home/domain.com/public_html/index.html
chown -R user-name:group-name /home/domain.com/public_html/*

### Step 7: Starting OpenLiteSpeed

To start OpenLiteSpeed, use the following command:

systemctl start lsws

### Step 8: Configuring WebAdmin Console

To access the OpenLiteSpeed web-based administration console, you need to set up the login credentials. Execute the following command:

/usr/local/lsws/admin/misc/admpass.sh

You can now log in to the webadmin console using the URL https://your_server_ip:7080. Make sure that port 7080 is not blocked by your firewall.

### Step 9: Optimizing OpenLiteSpeed Performance

To optimize the performance of OpenLiteSpeed, you can make a few adjustments in the server configuration. Follow these steps:

Open the webadmin console and navigate to Configuration > Listeners.

Locate the listener for your domain and click on it.

Adjust the following settings:

Address: uds://tmp/lshttpd/domain.sock
Max Connections: 10
Environment: PHP_LSAPI_CHILDREN=10
Command: /usr/local/lsws/lsphp74/bin/lsphp
Run As User: user-name
Run As Group: group-name

Note: If your website requires more PHP processes, you can gradually increase the values of Max Connections and PHP_LSAPI_CHILDREN.

### Step 10: Setting Up SSL/TLS Certificates

To secure your website with an SSL/TLS certificate, you can use acme.sh to obtain and install Let's Encrypt certificates. Execute the following commands:

curl https://get.acme.sh | sh
domain="domain.com"; /root/.acme.sh/acme.sh --issue -d "$domain" -d www."$domain" -w /home/"$domain"/public_html
Make sure to replace domain.com with your actual domain. If you don't use the www subdomain, you can remove the -d www."$domain" part.

### Step 11: Enforcing HTTPS Redirection

To force HTTPS redirection for your website, you can add a rewrite rule to your previously created .htaccess file. Edit the file and add the following lines:

RewriteEngine On
RewriteCond %{HTTPS} !=on
RewriteRule ^/?(.*) https://%{SERVER_NAME}/$1 [R=301,L]
Make sure to restart OpenLiteSpeed for the changes to take effect.

Congratulations! You have successfully installed and configured OpenLiteSpeed on CentOS 7. Your website should now benefit from improved performance and security.

Source: [Cara Install Openlitespeed](https://kumiskiri.com/cara-install-openlitespeed-ubuntu/)
