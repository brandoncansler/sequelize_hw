# Sequelize Homework: Reverse Engineering Code

* This app allows users to create an account, log into the account and sign back out securely. All user data is stored in a mysql
database.


#### User Story

```
AS A person who wants to use an app

I WANT to know my info is safely stored

SO THAT I may safely use the app
```


#### Technology Used 
(may be viewed in package.json under dependencies)

- bcryptJS
- express
- express-session
- mySQL2
- passport
- sequelize


## Before Using The App

#### to begin using this app, please follow these steps:

1) create a database called "passport_demo" in mySQL

2) open the config.js file in config and insert your password under development if you have one

3) open your terminal and run `npm i` or `npm install` to install all node packages

4) still in terminal, run `node server.js` or `npm start` to launch the app

5) proceed to "http://localhost:8080" in your browser

## File Breakdown

### config

* **config.json** connection configuration to server.
  
* **passport.js** contains the javascript logic telling *passport* we want to use an email address and password to login.

#### middleware
  
* **isAuthenticated.js** restricts the routes that the user is allowed to visit so that only if the user is properly loggin in will it execute the given requests

- - -
    
### models

* **index.js** connects to the database and imports the user login data.
  
* **user.js** requires *bcrypt* with `var bcrypt = require("bcryptjs");` for password hashing, this makes the database more secure even if it were to be compromised. Also in this file, we have javascript detailing our user info model for the database.

- - -
  
### routes

* **api-routes.js** provides the routes for signing in, logging out and getting the user data via *POST* and *GET* api requests

requires **models** and **passport.js** via `var db = require("../models");` & `var passport = require("../config/passport");` 
  
* **html-routes.js** provides the routes that verify if the user is signed in/if they have an account and then redirects them to the correct html page client side

requires *path* package via `var path = require("path");` as well as *isAuthenticated.js* via `var isAuthenticated = require("../config/middleware/isAuthenticated");`

- - -
  
### package.json

* package information, node modules used, etc.

- - -

### server.js

* requires packages (i.e. express and express-session)

* requires *passport* as it has been configured via `var passport = require("./config/passport");`

* establishes PORT for local host and/or deployment via `var PORT = process.env.PORT || 8080;`

* requires *models* for syncing via `var db = require("./models");`

* creating express app and configuring middleware needed for authentication using express and express sessions

* requires *html-routes* as well as *api-routes* via `require("./routes/html-routes.js")(app);` and `require("./routes/api-routes.js")(app);`

* syncing our database and logging a message to the user upon success using db.sequelzie and app.listen