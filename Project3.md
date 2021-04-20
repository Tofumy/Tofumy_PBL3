# Project 3

**Step 1** - Backend configuration
---

The below cmdlet update ubuntu

`$ sudo apt update`

![screenshot](https://github.com/Tofumy/Tofumy-PBL3/blob/main/sudo-update.JPG)

The below cmdlet upgrade ubuntu

`$ sudo apt upgrade`

![screenshot](https://github.com/Tofumy/Tofumy-PBL3/blob/main/sudo-upgrade.JPG)

We used the below to get the location of Node.js software from Ubuntu repositories.

`curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -`

![screenshot](https://github.com/Tofumy/Tofumy-PBL3/blob/main/nodejs-location.JPG)


## Install Nodejs on the server

Installed Node.js with the command below

`sudo apt-get install -y nodejs`

![screenshot](https://github.com/Tofumy/Tofumy-PBL3/blob/main/install-node.JPG)

We verified the node and npm installation with the commands below

`node -v` 

`npm -v` 

![screenshot](https://github.com/Tofumy/Tofumy-PBL3/blob/main/node-npm-ver.JPG)

















![screenshot](https://github.com/Tofumy/Tofumy-PBL2/blob/main/sudo-apt1.JPG)

![screenshot](https://github.com/Tofumy/Tofumy-PBL2/blob/main/sudo-apt-install.JPG)

We used the below cmdlet to confirm that Nginx server is active

`$ sudo systemctl status nginx`

![screenshot](https://github.com/Tofumy/Tofumy-PBL2/blob/main/systemctl-status.JPG)

Enabled the TCP Port 22 for the EC2 instance

![screenshot](https://github.com/Tofumy/Tofumy-PBL2/blob/main/inbound-rule.JPG)

We just used it to confirm if we can access the nginx server locally 

`$ curl http://localhost:80`

![screenshot](https://github.com/Tofumy/Tofumy-PBL2/blob/main/curl-localhost.JPG)

`$ curl http://3.138.202.128:80`

![screenshot](https://github.com/Tofumy/Tofumy-PBL2/blob/main/curl-publicip.JPG)

We tried to access the public Ip over the browser and below is the output

![screenshot](https://github.com/Tofumy/Tofumy-PBL2/blob/main/browser-nginx.JPG)




**Step 2** - Installing MySQL

The below cmdlet installs the mysql in the server

`$ sudo apt install mysql-server`

![screenshot](https://github.com/Tofumy/Tofumy-PBL2/blob/main/install-mysql.JPG)

The below cmdlet runs a security script that removes insecure default settings and lock down access to the database system

`$ sudo mysql_secure_installation`

![screenshot](https://github.com/Tofumy/Tofumy-PBL2/blob/main/secure-sql.JPG)


This code verifies that we can log in to the MySQL server

`$ sudo mysql`

![screenshot](https://github.com/Tofumy/Tofumy-PBL2/blob/main/test-mysql.JPG)



**Step 3** - Installing PHP

The below cmdlet installs *php-fpm* (PHP fastCGI process manager) and *php-msql* (PHP module to communicate with MySQL-based databases)

`$ sudo apt install php-fpm php-mysql`

![screenshot](https://github.com/Tofumy/Tofumy-PBL2/blob/main/php-install.JPG)


