---
title: "How to Install Nginx Ubuntu 20.04 Server and Desktop: 6 Step Easy"
description: "Learn how to install Nginx on Ubuntu 20.04 Server and Desktop effortlessly. Step-by-step guide for a seamless installation experience."
date: "2023-07-03"
categories:
- "Nginx"
---

Are you looking to [install Nginx Ubuntu 20.04](https://kumiskiri.com/install-nginx-ubuntu/) server and desktop? In this comprehensive guide, we will walk you through the step-by-step process of installing Nginx on both your server and desktop environments. Nginx is a popular web server that offers high performance and scalability, making it a great choice for hosting websites and applications. By following this tutorial, you will have Nginx up and running in no time, ready to serve your web content efficiently.

## Install Nginx Ubuntu 20.04

A number of steps that you must follow so that the Install Nginx Ubuntu 20.04 Server and Desktop process runs successfully, do it carefully

### Step 1: Updating Software Packages

To begin the installation process of the LEMP stack on your Ubuntu 20.04 server or desktop, it's important to ensure that all software packages are up to date. Follow the commands below to update your system:

sudo apt update
sudo apt upgrade

### Step 2: Installing Nginx Web Server

Nginx is a powerful and efficient web server that will serve as the backbone of your LEMP stack. Execute the following commands to install and configure Nginx:

sudo apt install nginx
sudo systemctl enable nginx
sudo systemctl start nginx
sudo systemctl status nginx

To verify the installation and check the Nginx version, run the following command:

nginx -v

### Step 3: Installing MariaDB Database Server

MariaDB will act as the database management system for your LEMP stack. Follow the commands below to install MariaDB:


sudo apt install mariadb-server mariadb-client
systemctl status mariadb
sudo systemctl start mariadb
sudo systemctl enable mariadb
sudo mysql_secure_installation

To verify the installation and check the MariaDB version, execute the following command:

mariadb --version

### Step 4: Installing PHP7.4

PHP is a popular programming language used for server-side scripting in web development. To install PHP7.4 and its necessary extensions, use the following commands:

sudo apt install php7.4 php7.4-fpm php7.4-mysql php-common php7.4-cli php7.4-common php7.4-json php7.4-opcache php7.4-readline php7.4-mbstring php7.4-xml php7.4-gd php7.4-curl
sudo systemctl start php7.4-fpm
sudo systemctl enable php7.4-fpm

### Step 5: Creating an Nginx Server Block

Next, you need to create an Nginx server block to configure the website's settings. Use the commands below to accomplish this:

sudo rm /etc/nginx/sites-enabled/default
sudo nano /etc/nginx/conf.d/default.conf

Within the text editor, paste the following configuration block:

nginx

server {
  listen 80;
  listen [::]:80;
  server_name _;
  root /usr/share/nginx/html/;
  index index.php index.html index.htm index.nginx-debian.html;

  location / {
    try_files $uri $uri/ /index.php;
  }

  location ~ \.php$ {
    fastcgi_pass unix:/run/php/php7.4-fpm.sock;
    fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
    include fastcgi_params;
    include snippets/fastcgi-php.conf;
  }

  location ~* \.(jpg|jpeg|gif|png|webp|svg|woff|woff2|ttf|css|js|ico|xml)$ {
    access_log off;
    log_not_found off;
    expires 360d;
  }

  location ~ /\.ht {
    access_log off;
    log_not_found off;
    deny all;
  }
}

To validate the Nginx configuration, run the following command:


sudo nginx -t

Finally, reload Nginx for the changes to take effect:


sudo systemctl reload nginx

### Step 6: Testing PHP

To ensure that PHP is working correctly with Nginx, follow the steps below:

sudo nano /usr/share/nginx/html/info.php
Inside the text editor, add the following code:

<?php phpinfo(); ?>

Save the file and exit the text editor. Then, remove the info.php file for security purposes:

sudo rm /usr/share/nginx/html/info.php

Troubleshooting Tip

If you encounter any issues or need to restart Nginx, use the following commands:


sudo systemctl restart nginx
sudo mkdir -p /etc/systemd/system/nginx.service.d/
sudo nano /etc/systemd/system/nginx.service.d/restart.conf

Within the text editor, add the following lines:

[Service]
Restart=always
RestartSec=5s

Save the file and execute the following commands to reload the daemon and restart Nginx:

sudo systemctl daemon-reload
sudo pkill nginx
systemctl status nginx

By following these steps, you have successfully installed the LEMP stack (Nginx, MariaDB, and PHP7.4) on your Ubuntu 20.04 server or desktop. Enjoy building and deploying your web applications with this powerful software stack!
