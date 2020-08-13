# Code Snippets for Quick Node.js App Setup    

After setting up a node.js app (run npm init), the following code can be added to your app.js file.
-------




## All-encompassing node.js app config    

```
const express = require("express"),
      bodyParser = require("body-parser"),
      methodOverride = require("method-override"),
      mongoose = require("mongoose"),
      passport = require('passport'),
      localStrategy = require('passport-local'),
      passportLocalMongoose = require('passport-local-mongoose'),
      session = require('express-session');
      
const app = express();

// Middleware
app.set('view engine', "ejs");
app.use(express.static("public"));
app.use(bodyParser.urlencoded({extended: true}));
app.use(methodOverride("_method"));

// Setup passport
app.use(session({
    secret: 'Def Leppard is the GOAT',
    resave: false,
    saveUninitialized: false
}));
app.use(passport.initialize());
app.use(passport.session());
passport.use(new localStrategy(User.authenticate()));
passport.serializeUser(User.serializeUser());
passport.deserializeUser(User.deserializeUser());

```      
## Basic Setup   

```
const express = require("express"), // express routing
      bodyParser = require("body-parser"), // Parses user input
      methodOverride = require("method-override"); // enable more http requests (i.e. DELETE)
      
app.set('view engine', "ejs"); // Allows references to .ejs files without using the file extension
// Required config
app.use(bodyParser.urlencoded({extended: true}));
app.use(methodOverride("_method"));    


// At the end of the app.js file
app.listen(3000, () => {
      console.log("the app is running");
};
```


## Setup Mongoose
(To interact with MongoDB)   

```
const mongoose = require("mongoose");
const uri = "mongodb+srv://<username>:<password>@cluster0.vmffh.mongodb.net/resume?retryWrites=true&w=majority";
mongoose.connect(uri, {useNewUrlParser: true, useUnifiedTopology: true}).catch(error => handleError(error));
```    

## Setup Passport.js
(To add user authentication)   

```
const passport = require('passport'),
      localStrategy = require('passport-local'), // For custom authentication
      passportLocalMongoose = require('passport-local-mongoose') // Access MongoDB to save user auth details

app.use(session({
    secret: 'anything you want!',
    resave: false,
    saveUninitialized: false
}));
app.use(passport.initialize());
app.use(passport.session());
passport.use(new localStrategy(User.authenticate()));
passport.serializeUser(User.serializeUser());
passport.deserializeUser(User.deserializeUser());
```
  
