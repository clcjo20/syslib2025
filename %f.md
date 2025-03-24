# Steps and Installation of Apache , MySQL, PhP

Installation

Before we install Apache, we need to update our systems first. This ensures we will be downloading and installing the most recent, secure version of the package.

sudo apt update
sudo apt -y upgrade
Once the machine is updated, we can install Apache using apt. First we'll use apt search to identify the specific package name. I know that a lot of results will be returned, so I will pipe | the output from apt search command through the head command to look at the initial results:

apt search apache2 | head
The package that we're interested in happens to be named apache2 on Ubuntu. The name of this package is not a given, though. On other distributions, like Fedora, the Apache package is called httpd. This is why it's important to learn and use apt search <package_name> and apt show <package_name> commands to locate desired packages before installing.

apt show apache2
Once we've confirmed that apache2 is the package that we want, install it with the apt install <package_name> command. Press Y to agree to continue after running the command below:

sudo apt install apache2
Basic checks

Once it is installed, we need to make sure the server is up and running, configure some basic things, and create a basic web site.

To start, I use the systemctl command to acquire status info about apache2 and make sure it is enabled and running:

systemctl status apache2
The output may be overwhelming at first glance, so I advise you to read each line slowly. In particular, look for key lines that show its Active and Loaded status. For example, the output shows that apache2 is enabled, which is the default for this software. The term enabled means that the software starts automatically on reboot. The output should also state that the software is active. This means that the apache2 is running and live.


#Installing and Configuring PHP

Introduction

Client-side programming languages, like JavaScript, are handled entirely by the browser. To do this, browsers like Firefox, Chrome, Safari, Edge, and others include JavaScript engines that use just-in-time compilers to execute JavaScript code (see JavaScript Engine, Mozilla).

From an end user's perspective, you basically install JavaScript when you install a web browser.

PHP, on the other hand, is a server-side programming language. This means it must be installed on the server. Unlike with JavaScript, the browser does not execute PHP directly; instead, the web server processes the PHP and sends the resulting HTML or other content to the browser.

From a system or web administrator's perspective, this means that PHP has be installed and configured to work with the web/HTTP server. In our case, we have to install and configure PHP on our virtual instances to work with the Apache web server software.

One of the primary uses of PHP is to interact with databases, like MySQL, MariaDB, PostgreSQL, etc., in order to create data-based page content. To begin to set this up, we have to:

Install PHP and relevant Apache modules
Configure PHP and relevant modules to work with Apache
Configure PHP and relevant modules to work with MySQL
Install PHP

As usual, we will use apt install to install PHP and relevant modules. Then we will restart Apache using the systemctl command. Use apt show [package_name] to read more about each package we will install. The first command below installs the php and the libapache2-mod-php packages. The latter package is used to create a connection between PHP and the Apache web server.

sudo apt install php libapache2-mod-php
sudo systemctl restart apache2
Once installed, you want to confirm the installed version with the following command. This is because other software (e.g., WordPress, etc.) might require a specific version before that other software to work.

php -v
After we restart Apache, we need to check its status and see if there are any errors in the log output:

systemctl status apache2
Check Install

Next we check that PHP has been installed and that it's working with Apache. We can create a small PHP file in our web document root. To do that, we cd to the document root, /var/www/html/, and create a file called info.php:

cd /var/www/html/
sudo nano info.php
In that file, add the following text, then save and close the file:

<?php
phpinfo();
?>
Now visit that file using the public IP address for your server. If the public IP address for my virtual machine is 55.333.55.33, then in Firefox, Chrome, etc, I would open:

http://55.333.55.333/info.php

Once you've confirmed that PHP is installed and functioning, you should delete it since it exposes detailed systems information:

sudo rm /var/www/html/info.php




#Installing and Configuring MySQL

Introduction

We started our LAMP stack when we installed Apache on Linux. We added extra functionality when we installed and configured PHP to work with Apache. In this section, our objective is to complete the LAMP stack and install and configure MySQL.

If you need a refresher on relational databases, see: Introduction to Relational Databases. However in the next section, we will explore the database basics from the command line.

Install and Set Up MySQL

In this section, we'll learn how to install, setup, secure, and configure the MySQL relational database so that it works with the Apache web server and the PHP programming language.

First, as normal, we make run the following commands to ensure our machines are fully updated:

sudo apt update
sudo apt upgrade
sudo apt autoremove
sudo apt clean
Note that sometimes you will have to reboot your machine, mostly when you get a Linux kernel update. To do so, run sudo reboot now. This command will disconnect you from your machine. Wait a minute or two, and then reconnect.

Then we install the MySQL Community Server package. The MySQL Community Server package is a metapackage that installs the latest, most secure version of MySQL, regardless of the software's version number, as well as its dependencies.

sudo apt install mysql-server
The above install should be fine for us, but note that in some cases you first may want to specifically confirm which versions are available via the apt command since some software (e.g., WordPress) may require specific versions or above. You can check that with the following:

apt policy mysql-server
After installing, you can confirm the version number with the following command to ensure you know which version you are using:

mysql --version
The install process should start and enable the database server, but we can check if it's running and enabled using the systemctl command. Note that you are looking for the lines beginning with Loaded and Active.

systemctl status mysql 
Next we need to run a post installation script called mysql_secure_installation. The script performs some security checks and creates a secure, baseline configuration of MySQL. To do that, run the following command:

sudo mysql_secure_installation
When you run the above script, you'll get a series of prompts to respond to. For most responses, you will want to respond with a Y for yes. We will respond with a Y to the first question on validating passwords, but to keep things simple, select LOW when prompted for the password validation policy. This will enforce a weak password policy for testing, but note that in real-world scenarios, we might want to select a more secure policy. In the output below, I show how to respond to each question:

Validate passwords: Y
Password validation policy: 0 (zero) for LOW
Remove anonymous users: Y
Disallow root login remotely: Y
Remove test database and access to it: Y
Reload privilege tables now: Y
We can login to the database now. In order to do so, we use the following command:

sudo mysql -u root
NOTE: we need to distinguish between the regular user prompt of our Linux accounts and the MySQL prompt below. The default prompt for our user accounts has the following syntax: user_name@computer_name:path$ . In the following, I will indicate we are at the MySQL prompt with the following text: mysql>. Do not type that prompt when you are using MySQL.
