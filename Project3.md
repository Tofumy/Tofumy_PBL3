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

In the "Todo" directory, installed Mongoose

`npm install mongoose`

![screenshot](https://github.com/Tofumy/Tofumy_PBL3/blob/main/install-mongoose.JPG)


Created a new directory within the "Todo" folder and created a new file "todo.js" 

`mkdir models && cd models && touch todo.js`

![screenshot](https://github.com/Tofumy/Tofumy_PBL3/blob/main/mkdir-models-todojs.JPG)

Opened the file with this `vim todo.js` using the vim text editor and pasted the code below in the file:

``` javascript

const mongoose = require('mongoose');
const Schema = mongoose.Schema;

//create schema for todo
const TodoSchema = new Schema({
action: {
type: String,
required: [true, 'The todo text field is required']
}
})

//create model for todo
const Todo = mongoose.model('todo', TodoSchema);

module.exports = Todo;

```

![screenshot](https://github.com/Tofumy/Tofumy_PBL3/blob/main/vim-todojs.JPG)

In the Routes directory, opened *api.js* with `vim api.js`, deleted the code inside with *:%d* command and pasted the below:

``` javascript

const express = require ('express');
const router = express.Router();
const Todo = require('../models/todo');

router.get('/todos', (req, res, next) => {

//this will return all the data, exposing only the id and action field to the client
Todo.find({}, 'action')
.then(data => res.json(data))
.catch(next)
});

router.post('/todos', (req, res, next) => {
if(req.body.action){
Todo.create(req.body)
.then(data => res.json(data))
.catch(next)
}else {
res.json({
error: "The input field is empty"
})
}
});

router.delete('/todos/:id', (req, res, next) => {
Todo.findOneAndDelete({"_id": req.params.id})
.then(data => res.json(data))
.catch(next)
})

module.exports = router;

```

![screenshot](https://github.com/Tofumy/Tofumy_PBL3/blob/main/new-apijs1.JPG)

![screenshot](https://github.com/Tofumy/Tofumy_PBL3/blob/main/new-apijs.JPG)



### MongoDB Database

Created a Mongo DB using a DBaaS mLab which can be gotten from this link [mLab](https://www.mongodb.com/atlas-signup-from-mlab)


In the *index.js* file, we specified *process.env* to access environment variables, so we have to create the process.env file

Created a file in the *Todo directory* and named it .env.

`touch .env`

`vi .env`

![screenshot](https://github.com/Tofumy/Tofumy_PBL3/blob/main/vi-env.JPG)


Added the connection string to access the database in it, using the below:

`DB = mongodb+srv://Tofumy:<password>@cluster1.qcl1a.mongodb.net/myFirstDatabase?retryWrites=true&w=majority`

![screenshot](https://github.com/Tofumy/Tofumy_PBL3/blob/main/mongodb-connect.JPG)





<!--mLab, DB:u=Tofumy p=damilola18 mLab console: u=Tofumy p=damilola18  -->
