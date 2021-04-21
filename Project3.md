# Project 3

**Step 1** - Backend configuration
---

The below cmdlet update ubuntu

`$ sudo apt update`

![screenshot](https://github.com/Tofumy/Tofumy_PBL3/blob/main/sudo-update.JPG)

The below cmdlet upgrade ubuntu

`$ sudo apt upgrade`

![screenshot](https://github.com/Tofumy/Tofumy_PBL3/blob/main/sudo-upgrade.JPG)

We used the below to get the location of Node.js software from Ubuntu repositories.

`curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -`

![screenshot](https://github.com/Tofumy/Tofumy_PBL3/blob/main/nodejs-location.JPG)


### Install Nodejs on the server

Installed Node.js with the command below

`sudo apt-get install -y nodejs`

![screenshot](https://github.com/Tofumy/Tofumy_PBL3/blob/main/install-node.JPG)

We verified the node and npm installation with the commands below

`node -v` 

`npm -v` 

![screenshot](https://github.com/Tofumy/Tofumy_PBL3/blob/main/node-npm-ver.JPG)


### Application Code Setup

Created a new directory for your To-Do project:

`mkdir Todo`

Ran the command below to verify that the Todo directory is created:

`ls`

Changed the current directory to the newly created one:

`cd Todo`

![screenshot](https://github.com/Tofumy/Tofumy_PBL3/blob/main/mkdir-todo.JPG)

Used the command `npm init` to initialise the project and to create a *package.json* will be created.

![screenshot](https://github.com/Tofumy/Tofumy_PBL3/blob/main/npm-init.JPG)

and then used `ls` to confirm if the package


### Install ExpressJS

Installed *express js* using npm:

`npm install express`

Created a file index.js with the command below:

`touch index.js`

Then use the `ls` to confirm if the file is created

![screenshot](https://github.com/Tofumy/Tofumy_PBL3/blob/main/install-expressjs.JPG)

Installed the *dotenv module*

`npm install dotenv`

![screenshot](https://github.com/Tofumy/Tofumy_PBL3/blob/main/install-dotenv.JPG)

Opened the index.js file with the command below

`vim index.js`

Typed the code below into it and save. 

``` javascript

const express = require('express');
require('dotenv').config();

const app = express();

const port = process.env.PORT || 5000;

app.use((req, res, next) => {
res.header("Access-Control-Allow-Origin", "\*");
res.header("Access-Control-Allow-Headers", "Origin, X-Requested-With, Content-Type, Accept");
next();
});

app.use((req, res, next) => {
res.send('Welcome to Express');
});

app.listen(port, () => {
console.log(`Server running on port ${port}`)
});

```

![screenshot](https://github.com/Tofumy/Tofumy_PBL3/blob/main/vim-indexjs.JPG)

Note:
in vim, use *:w* to save
        use *:qa* to exit

Tested our server using the below cmdlets:

`node index.js`

![screenshot](https://github.com/Tofumy/Tofumy_PBL3/blob/main/test-node.JPG)

Created a custom inbound rule to allow port 5000 in the EC2 instance:

![screenshot](https://github.com/Tofumy/Tofumy_PBL3/blob/main/custom-inbound-rule.JPG)

Tried to access the server’s Public IP to test the Express JS

![screenshot](https://github.com/Tofumy/Tofumy_PBL3/blob/main/testing-node-public.JPG)

### Create Routes

**There are three actions to do for the To-Do application**

- Create a new task
- Display list of all tasks
- Delete a completed task

Created routes directory

`mkdir routes`

Changed directory to routes folder.

`cd routes`

Created a file *api.js* with the command below

`touch api.js`

![screenshot](https://github.com/Tofumy/Tofumy_PBL3/blob/main/create-routes-api.JPG)


Opened the file with the command below

`vim api.js`

``` javascript

const express = require ('express');
const router = express.Router();

router.get('/todos', (req, res, next) => {

});

router.post('/todos', (req, res, next) => {

});

router.delete('/todos/:id', (req, res, next) => {

})

module.exports = router;

```

![screenshot](https://github.com/Tofumy/Tofumy_PBL3/blob/main/vim-apijs.JPG)




---

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


