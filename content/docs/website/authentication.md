---
title: "Authentication"
description: "feff"
summary: ""
date: 2025-12-19T08:27:10+02:00
lastmod: 2025-12-19T08:27:10+02:00
draft: false
weight: 911
toc: true
seo:
  title: "" # custom title (optional)
  description: "" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  noindex: false # false (default) or true
---

## 1. Overview
The application in the Server Setup can currently only be used by one person. Therefore, adding a login and register page will allow multiple user to user different sessions simultaneously. To implement this, we utilise the sessions library. However, each user will require username and password to create a session. To implement the authentication mechanism, we use the PassportJS library.

### Learning Goals
- Create a Login and Registration Page to allow multiple Users to access the app.
- Understand and Implement **Sessions** for those Users.

## 2. Passport.js Overview
Passport.js is an authentication middleware for Node.js that provides a simple and flexible way to handle user authentication. It supports a wide range of authentication strategies, including:

Local authentication (username and password)
OAuth (e.g., Google, Facebook, GitHub)
OpenID
JWT (JSON Web Tokens)
Passport.js is highly modular, allowing developers to choose the strategies that best fit their application’s needs.
We will be utilising the Local Authentication Stratergy.

## 3. Dependencies
Install the following NPM Dependencies:
```
npm install express passport passport-local express-session bcrypt
```
- express: A web framework for Node.js.
- passport: The core Passport.js library.
- passport-local: A strategy for authenticating with a username and password.
- express-session: Middleware for managing user sessions.
- bcrypt: A library for hashing passwords.

## 4. Database Tables
Create a Table in the database for Users and Sessions via the terminal:
```sql
CREATE TABLE IF NOT EXISTS `User` (
  `id` INT AUTO_INCREMENT PRIMARY KEY,
  `first_name` VARCHAR(45) NOT NULL,
  `last_name` VARCHAR(45) NOT NULL,
  `email` VARCHAR(255) NOT NULL UNIQUE,
  `password` VARCHAR(255) NOT NULL,
  'role' enum('admin','user') NOT NULL
);
```
```sql
CREATE TABLE IF NOT EXISTS `sessions` (
`session_id` varchar(128) COLLATE utf8mb4_bin NOT NULL, 
 `expires` int(11) unsigned NOT NULL, 
`data` mediumtext COLLATE utf8mb4_bin, 
PRIMARY KEY (`session_id`)
) ENGINE=InnoDB
```

## 5. Login and Registration Pages
### Login
`views/login.ejs`
```html
<div class="row mt-5">
    <div class="col-md-6 m-auto">
      <div class="card card-body">
        <h1 class="text-center mb-3"><i class="fas fa-sign-in-alt"></i>  Login</h1>
        <%- include('./partials/messages.ejs') %>
        <form action="/user/login" method="POST">
          <div class="form-group">
            <label for="email">Email</label>
            <input
              type="email"
              id="email"
              name="email"
              class="form-control"
              placeholder="Enter Email"
            />
          </div>
          <div class="form-group">
            <label for="password">Password</label>
            <input
              type="password"
              id="password"
              name="password"
              class="form-control"
              placeholder="Enter Password"
            />
          </div>
          <button type="submit" class="btn btn-primary btn-block">Login</button>
        </form>
        <p class="lead mt-4">
          No Account? <a href="/user/register">Register</a>
        </p>
      </div>
    </div>
  </div>
```
### Registration
`views/register.ejs`
```html
<div class="row mt-5">
    <div class="col-md-6 m-auto">
      <div class="card card-body">
        <h1 class="text-center mb-3">
          <i class="fas fa-user-plus"></i> Register
        </h1>
        <%- include('./partials/messages.ejs') %>
        <form action="/user/register" method="POST">
          <div class="form-group">
            <label for="name">First Name</label>
            <input
              type="first_name"
              id="first_name"
              name="first_name"
              class="form-control"
              placeholder="Enter First Name"
              value="<%= typeof name != 'undefined' ? name : '' %>"
            />
            <div class="form-group">
                <label for="last_name">Last Name</label>
                <input
                  type="last_name"
                  id="last_name"
                  name="last_name"
                  class="form-control"
                  placeholder="Enter Last Name"
                  value="<%= typeof name != 'undefined' ? name : '' %>"
                />
          </div>
          <div class="form-group">
            <label for="email">Email</label>
            <input
              type="email"
              id="email"
              name="email"
              class="form-control"
              placeholder="Enter Email"
              value="<%= typeof email != 'undefined' ? email : '' %>"
            />
          </div>
          <div class="form-group">
            <label for="password">Password</label>
            <input
              type="password"
              id="password"
              name="password"
              class="form-control"
              placeholder="Create Password"
              value="<%= typeof password != 'undefined' ? password : '' %>"
            />
          </div>
          <div class="form-group">
            <label for="password2">Confirm Password</label>
            <input
              type="password"
              id="password2"
              name="password2"
              class="form-control"
              placeholder="Confirm Password"
              value="<%= typeof password2 != 'undefined' ? password2 : '' %>"
            />
          </div>
          <button type="submit" class="btn btn-primary btn-block">
            Register
          </button>
        </form>
        <p class="lead mt-4">Have An Account? <a href="/user/login">Login</a></p>
      </div>
    </div>
  </div>
```

## 6.  Controllers
Create a Controller to Retrieve and Insert Users.

`controllers/UserController.js`
```js
import mysql from 'mysql2'
import dotenv from 'dotenv';
dotenv.config()
 
const pool = mysql.createPool({
    connectionLimit: 10,
    password: process.env.MYSQL_USER_PASSWORD,
    user: process.env.MYSQL_USER_USER,
    database: process.env.MYSQL_USER_DATABASE,
    host: process.env.MYSQL_HOST,

});
 
export async function getUser(id) {
    return new Promise((resolve, reject)=>{
        pool.query('SELECT * FROM User WHERE id= ?', [id], (error, user)=>{
            if(error){
                return reject(error);
            }
            return resolve(user);
        });
    });
};
 
export async function getUserByEmail(email) {
    return new Promise((resolve, reject)=>{
        pool.query('SELECT * FROM User WHERE email = ?', [email], (error, users)=>{
            if(error){
                return reject(error);
            }
            return resolve(users[0]);
        });
    });
};

export async function insertUser (first_name, last_name, email, password) {
    return new Promise((resolve, reject)=>{
        pool.query('INSERT INTO User (first_name, last_name, email, password,role) VALUES (?, ?, ?,?,?)', [first_name, last_name, email, password,'user'], (error, result)=>{
            if(error){
                return reject(error);
            }
             
              return resolve(result.insertId);
        });
    });
};
```

## 7. Sessions
Modify the `app.js` file to initialize a unique session for each user.
```js
const express = require('express');
const session = require('express-session');
const passport = require('passport');
const LocalStrategy = require('passport-local').Strategy;
const bcrypt = require('bcrypt');
const app = express();
const PORT = 3000;

// Middleware
app.use(express.urlencoded({ extended: true }));
app.use(session({
  secret: 'your-secret-key',
  resave: false,
  saveUninitialized: false,
}));
app.use(passport.initialize());
app.use(passport.session());

// Routes
app.get('/', (req, res) => {
  res.send('Welcome to the home page!');
});

app.listen(PORT, () => {
  console.log(`Server is running on http://localhost:${PORT}`);
});
```

## 8. Passport.js Config
Local Stratergy Flow:
- The Local Statergy will receive a Username and Password from the Login page.
- It will compare the Username to the Users database and if it does not find the User, it will throw an error.
- If it finds the User, it will compare the Hash of the Users Password to the Hash stored in the Database.
- If it does not match, it will throw an error, else it will return the User.
- The stratergy serializes a new and unique session when a person logs in and deserializes it when the person logs out.

`config/passport.js`
```js
import Strategy from 'passport-local'
import bcrypt from 'bcryptjs'
import { getUserByEmail,getUser } from '../controllers/userController.js'

const LocalStrategy = Strategy.Strategy

export function PassportFunc(passport) {
    passport.use(new LocalStrategy({usernameField: 'email'}, async (email, password, done) => {
        try {
            const user = await getUserByEmail(email);

            if (!user) {
                return done(null, false, { message: 'No user found with that email' });
            }

            const isMatch = await bcrypt.compare(password, user.password);

            if (!isMatch) {
                return done(null, false, { message: 'Password incorrect' });
            }

            return done(null, user);
        } catch (error) {
            console.error(error);
            return done(error);
        }
    }));

    passport.serializeUser((user, done) => {
        done(null, user.id);
    });
    passport.deserializeUser(async (id, done) => {
        try {
            const user = await getUser(id);
            done(null, user);
        } catch (error) {
            console.error(error);
            done(error);
        }
    });
}
```

## 9. Prevent unauthenticated access
The following code ensures that only users with a valid session can access the specific restricted pages:

`routes/user.js`
```js
routerUser.post('/login', (req, res, next) => {
    passport.authenticate('local', {
        successRedirect: '/dashboard',
        failureRedirect: '/user/login',
        failureFlash: true
    })(req, res, next);
})
```

## 10. Quickstart

{{< callout context="note" title="Github" icon="outline/info-circle" >}}
Clone the [Github Repo](https://github.com/jaimeen12/NodeJS-Passport) and run the following commands:

```bash
git clone https://github.com/jaimeen12/NodeJS-Passport
npm init -y
npm install
node app.js
```

{{< /callout >}}