---
title: "Functionality"
description: "cwdc"
summary: ""
date: 2025-12-19T02:27:10+02:00
lastmod: 2025-12-19T02:27:10+02:00
draft: false
weight: 912
toc: true
seo:
  title: "" # custom title (optional)
  description: "" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  noindex: false # false (default) or true
---

## 1. Overview

Building on the basic **CRUD** application, the following features are added to the project to increase the functionality:
- **File Uploads**: Users are allowed to upload their study notes to their tracker.
- **Portswigger**: Users can automatically keep track of their progress in the Port Swigger Academy via the web app.

### Learning Goals
- Understand how File Uploads work on a web server
- Understand how Web Scrapping works and how the DOM operates.

## 2. File Upload

### Multer
Multer is a middleware for handling multipart/form-data, which is primarily used for uploading files. It integrates seamlessly with Express and provides a convenient way to handle file uploads. 

Why use Multer:
- File Upload to a Specified Location
- Limit File Upload Size
- Filter on File Types


### File Upload Controller
```js
import multer from 'multer';
import path from 'path';
import fs from 'fs';

export function checkFileType(file, cb) {
    // Allowed file extensions
    const filetypes = /jpeg|jpg|png|gif|pdf/;
    // Check extension
    const extname = filetypes.test(path.extname(file.originalname).toLowerCase());
    // Check mime type
    const mimetype = filetypes.test(file.mimetype);
  
    if (mimetype && extname) {
      return cb(null, true);
    } else {
      cb('Error: Images or PDFs Only!');
    }
}

export async function upload() {

    const destination= `uploads/${user}/`;

// Set up storage engine
    const storage = multer.diskStorage({
        destination: destination,
        filename: function(req, file, cb) {
        cb(null, file.fieldname + '-' + Date.now() + path.extname(file.originalname));
        }
    });

    // Init upload
    const upload = multer({
        storage: storage,
        limits: { fileSize: 1000000 }, // Limit file size to 1MB
        fileFilter: function(req, file, cb) {
        checkFileType(file, cb);
        }
    }).single('myImage');

}
```

## 3. Web Scraper

### Puppeteer

Puppeteer is a Node.js library that lets you automate and control a Chrome/Chromium browser using JavaScript. It’s used for tasks like web automation, testing, and web scraping.

You use Puppeteer to scrape websites because it behaves like a real browser, which makes it effective for modern, dynamic sites. It can accesses dynamic content. It waits for elements that load after page render (AJAX, infinite scroll, pop-ups). It also mimics real user actions like clicking buttons, scrolling, typing, and log in, which HTTP requests can’t do.

The Portswigger Website does not have an API, therefore webscraping is used. However, if you are using other sites such as HackTheBox or TryHackMe, there are APIs which can be used to simplify the process.

### Web Scrapper Controller
```js
import puppeteer from 'puppeteer';

export async function getPortswigger (email, password)  {
    // Launch the browser and open a new blank page
    const browser = await puppeteer.launch({
         headless: true, 
         defaultViewport: {
            width: 1100,
            height: 1000
        }
    });
    const page = await browser.newPage();
    

    // Navigate the page to a URL
    await page.goto('https://portswigger.net/users',{waitUntil: 'load', timeout: 0});
    await page.waitForSelector('#EmailAddress')
    await page.type("#EmailAddress", email)
    await page.waitForSelector('#Password')
    await page.type("#Password", password)
    await page.click("#Login");
    await page.waitForNavigation()
    await page.goto("https://portswigger.net/web-security/all-labs",{waitUntil: 'load', timeout: 0});

   const paragraph2 = await page.evaluate(() => {
        const bookElements2 = document.querySelectorAll(".widgetcontainer-lab-link.is-notsolved");
        return Array.from(bookElements2).map((book) => {
            const title = book.querySelector('.flex-columns a').innerText;
            const status = book.querySelector('.lab-status-icon').innerText;
            return {title,status};
        })
})
        return paragraph2

};
```

## 4. Quickstart

{{< callout context="note" title="Github" icon="outline/info-circle" >}}
Clone the [Github Repo](https://github.com/jaimeen12/NodeJS-Passport) and run the following commands:

```bash
git clone https://github.com/jaimeen12/NodeJS-Passport
npm init -y
npm install
node app.js
```

{{< /callout >}}