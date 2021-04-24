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


Updated the *index.js* to reflect the use of *.env* so that *Node.js* can connect to the database.


Open the file with `vim index.js`

- Press esc
- Type :
- Type %d
- Hit ‘Enter’
the whole content was deleted, then,

Pressed *i* to enter the insert mode in vim

Now, pasted the entire code below in the file.

``` javascript

const express = require('express');
const bodyParser = require('body-parser');
const mongoose = require('mongoose');
const routes = require('./routes/api');
const path = require('path');
require('dotenv').config();

const app = express();

const port = process.env.PORT || 5000;

//connect to the database
mongoose.connect(process.env.DB, { useNewUrlParser: true })
.then(() => console.log(`Database connected successfully`))
.catch(err => console.log(err));

//since mongoose promise is depreciated, we overide it with node's promise
mongoose.Promise = global.Promise;

app.use((req, res, next) => {
res.header("Access-Control-Allow-Origin", "\*");
res.header("Access-Control-Allow-Headers", "Origin, X-Requested-With, Content-Type, Accept");
next();
});

app.use(bodyParser.json());

app.use('/api', routes);

app.use((err, req, res, next) => {
console.log(err);
next();
});

app.listen(port, () => {
console.log(`Server running on port ${port}`)
});
Using environment variables to store information is considered more secure and best practice to separate configuration and secret data from the application, instead of writing connection strings directly inside the index.js application file.

```

![screenshot](https://github.com/Tofumy/Tofumy_PBL3/blob/main/new-vim-indexjs.JPG)


Started the server using the command:

`node index.js`


Below was a screen shot showing we connected to Database succesfully

![screenshot](https://github.com/Tofumy/Tofumy_PBL3/blob/main/node-test-db.JPG)






### Testing Backend Code without Frontend using RESTful API





**Step 2** - Frontend creation
---
 
We used the *create-react-app* command to scaffold our app.

In the Todo directory, I ran the below code which will create a "client directory" in the "Todo directory":

`npx create-react-app client`

![screenshot](https://github.com/Tofumy/Tofumy_PBL3/blob/main/npx-react-client.JPG)

Had to install some react js dependencies

Installed *concurrently* using the below: 

`npm install concurrently --save-dev`

Installed *nodemon* using the below:

`npm install nodemon --save-dev`

<!-- It is used to run and monitor the server. If there is any change in the server code, nodemon will restart it automatically and load the new changes. -->


We edited the *package.json* file (only the script section) using the vim text editor and pasted the below

``` javascript

"scripts": {
"start": "node index.js",
"start-watch": "nodemon index.js",
"dev": "concurrently \"npm run start-watch\" \"cd client && npm start\""
},

```

![screenshot](https://github.com/Tofumy/Tofumy_PBL3/blob/main/vim-package-json.JPG)


We need to configure Proxy in *package.json*

- Changed directory to ‘client’ using `cd client`
- Opened the package.json file using `vi package.json`
- Added the key value pair in the *package.json* file  `"proxy": "http://localhost:5000".`

![screenshot](https://github.com/Tofumy/Tofumy_PBL3/blob/main/proxy-package-json.JPG)

 
<!-- The whole purpose of adding the proxy configuration is to make it possible to access the application directly from the browser by simply calling the server url like http://localhost:5000 rather than always including the entire path like http://localhost:5000/api/todos -->

Change directory to the Todo folder and run the below:

`npm run dev`

Your app should open and start running on *localhost:3000*

![screenshot](https://github.com/Tofumy/Tofumy_PBL3/blob/main/npm-dev-run.JPG)

Created a custom inbound rule to allow port 3000

![screenshot](https://github.com/Tofumy/Tofumy_PBL3/blob/main/port3000.JPG)


<!-- ps aux | grep npm    that cmd helps to list processes running in the linux terminal -->

### Creating your React Components

<!-- One of the advantages of react is that it makes use of components, which are reusable and also makes code modular. For our Todo app, there will be two stateful components and one stateless component. --> 

- From the *Todo directory* ran `cd client` and moved to the *src* directory using `cd src`
- Inside the *src folder*, created another folder called *components* using `mkdir components`
- Changed directory to the *components* folder using `cd components`
- Inside the ‘components’ directory created three files *Input.js*, *ListTodo.js* and *Todo.js*.
`touch Input.js ListTodo.js Todo.js`

![screenshot](https://github.com/Tofumy/Tofumy_PBL3/blob/main/components-js.JPG)




