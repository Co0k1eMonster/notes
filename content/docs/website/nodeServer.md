---
title: "Server Setup"
description: "Reference pages are ideal for outlining how things work in terse and clear terms."
summary: ""
date: 2023-09-07T16:13:18+02:00
lastmod: 2023-09-07T16:13:18+02:00
draft: false
weight: 910
toc: true
seo:
  title: "" # custom title (optional)
  description: "" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  noindex: false # false (default) or true
---

## 1. Project Introduction
The project aims to create a Web Application which allows a beginner in the cybersecurity field to track the topics they are learning. The application allows a user to create a topic and track their progress in their studies and ensure that all topics are covered. The notes are stored in a database which ensures persistent storage.

## 2. Learning Goals

### Frontend:
The project is an implementation of knowledge in the following key areas:
- HTML
- CSS
- Javascript 

### Backend:
Implement a Node Server to consolidate the frontend technologies with data from a **MySQL** database. 


## 3. Functionality
  - Persistent storage
  - Create a note
  - Read a note
  - Update a note
  - Delete a note

## 4. Technical Implementation

### NodeJS and Express
- **NodeJS**:As an asynchronous event-driven JavaScript runtime, Node.js is designed to build scalable network applications.
- **Express**: A minimal web framework that runs on Node.js which makes routing, requests, responses and middleware easy by removing boilerplate code.

```js
const express = require('express');
const bodyParser = require('body-parser');
const app = express();
const PORT = process.env.PORT || 3000;

app.use(bodyParser.urlencoded({ extended: true }));
app.use(express.static('public'));

// Set up EJS as the view engine
app.set('view engine', 'ejs');

// Set up routes
const indexRoutes = require('./routes/index');
app.use('/', indexRoutes);

app.listen(PORT, () => {
  console.log(`Server is running on http://localhost:${PORT}`);
});
```

### MVC Structure
The MVC structure (Model–View–Controller) is used in Node.js apps to keep code organized, readable, and easy to maintain as your project grows.
| Part           | Responsibility                           |
| -------------- | ---------------------------------------- |
| **Model**      | Data & business logic (Database)                   |
| **View**       | What the user sees (HTML / EJS)          |
| **Controller** | Handles requests & connects Model + View |

#### MVC folder structure:
```css
src/
├── models/
│   └── Note.js
├── views/
│   ├── notes.ejs
│   ├── note.ejs
│   └── layout.ejs
├── controllers/
│   └── noteController.js
├── routes/
│   └── noteRoutes.js
├── app.js
```

### EJS and Partials
- **EJS**: It is a templating engine which allows you to insert Javascript variables and logic into HTML code(Views). The content is dynamically generated on the server side and sent to the client.
- **Partials**: Partials are pieces of HTML code which can be reused, therefore reducing redundancy in the code(DRY principle).
```js
// home.ejs
<%- include('./partials/head') %>
<%- include('./partials/header') %>
<div>
  <h2>The posts:</h2>
  <ul>
    <% posts.forEach((post)=> { %>
    <li>
      <a href="<%= post.link %>"><%= post.title %></a>
    </li>
    <% }) %>
  </ul>
</div>
<%- include('./partials/footer') %>
```

### Database
A MySQL database is configured with a table which stores the notes.

#### Installing MySQL
##### Mac
```
brew install mysql && brew services start mysql
```
##### Windows
Download and run the Community version of the MySQL Installer.

#### Login to MySQL
```
mysql -u root -p
```

mvc structure
mysql
bootstrap

#### Creating the Database Table
```sql
CREATE DATABASE notes;
USE notes;

CREATE TABLE IF NOT EXISTS `notes_table` (
`id` INT AUTO_INCREMENT PRIMARY KEY,
`title` VARCHAR(255) NOT NULL,
`status` enum('Pending', 'In Progress', 'Complete') NOT NULL,
`created_by` VARCHAR(255) NOT NULL
);
```

#### Styling
**Bootstrap**: Bootstrap helps you build good-looking, responsive websites faster, without needing to design everything from scratch. It provides preconfigured styles and components which provides a consistent and cohesive design. The code snippet below imports Bootstrap from a cdn which allows you to use the classes and components:

```html
<link
  href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css"
  rel="stylesheet"
/>
<script
  src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js"
></script>

```


## 5. Quickstart

{{< callout context="note" title="Github" icon="outline/info-circle" >}}
Clone the [Github Repo](https://github.com/jaimeen12/NodeJS-Passport) and run the following commands:

```bash
git clone https://github.com/jaimeen12/NodeJS-Passport
npm init -y
npm install
node app.js
```

{{< /callout >}}

