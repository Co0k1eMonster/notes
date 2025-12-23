---
title: "Roadmap to Junior Pentester"
description: "Guides lead a user through a specific task they want to accomplish, often with a sequence of steps."
summary: ""
date: 2023-09-07T16:04:48+02:00
lastmod: 2023-09-07T16:04:48+02:00
draft: false
weight: 810
toc: true
seo:
  title: "" # custom title (optional)
  description: "" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  noindex: false # false (default) or true
---

## The Chaos

Getting into penetration testing is exciting but it can also feel overwhelming. One quick search online and you’re hit with endless topics: networking, Linux, scripting, web apps, certifications, tools, exploits, and more. It’s easy to feel like you need to learn everything at once, which can be overwhelming. For many beginners, pentesting feels confusing, fragmented, and difficult to navigate.

At its core, pentesting is about understanding how complex systems work and how they can fail. Modern systems are built from many layers, and a pentester needs to understand several of them at once.

A single penetration test might involve:

- Networks and how data moves between systems
- Operating systems and how they manage users, processes, and permissions
- Web applications and how browsers interact with servers
- Databases and how data is stored and retrieved
- Security controls and how they are designed to stop attacks

The chaos is heightened when you hear advice such as:
- “Learn networking first”
- “Learn Linux”
- “Learn web security”
- “Learn scripting”
- “Just practice labs”

The hardest part of getting into penetration testing isn’t the technical difficulty—it’s the **Chaos**. There are too many topics, too many tools, too many opinions, and no obvious order to learn them in. Without structure, it’s easy to feel like you’re constantly busy but not actually progressing. All of this advice is technically correct—but without context, it feels overwhelming. Without strong foundations, learning can feel like memorizing random commands instead of developing real understanding. 

This is where a roadmap becomes powerful.

A roadmap doesn’t just tell you what to learn. Over time, it helps you build your own methodology—a way of thinking and approaching problems that brings order to complexity. Following a structured roadmap builds skills step by step, ensuring that there are no knowledge gaps and brings order to the chaos. 

## The Roadmap

The roadmap was developed by some of the best pentesters in South Africa to cultivate practical pentesting skills with an understanding of the fundemental concepts. The roadmap aims to develop real-world pentesting skills backed by industry-leading certifications.

![My photo](/roadmaptime.png)
![My photo](/roadmap.png)


## 1. Fundamentals

### Building a Website
Building a website is one of the best ways to gain foundational knowledge for penetration testing, even though it doesn’t look like “security” at first.

### Understanding How the Web Actually Works

When you build a website, you learn how the browser, server, and database interact with each other. This includes:
1. [A Basic Server Setup](https://)
2. [Authentication](https://)
3. [File Upload and Web Scraping](https://)
4. [Hosting the Website](https://)

### 1. A Basic Server Setup
The guide below shows you how to set up a NodeJS server with a MySQL Database to perform CRUD functions.
{{< link-card
  title="Basic Server Setup"
  description="Explore how to setup a basic server"
  href="/docs/website/server-setup/"
  target="_blank"
>}}

### 2. Authentication
We build on the basic server by allowing multiple users to access the app through a registration page where users can create profiles. The profiles are managed through sessions implemented by the PassportJS library.
{{< link-card
  title="Authentication"
  description="Explore how to configure authentication"
  href="/docs/website/authentication/"
  target="_blank"
>}}
### 3. Functionality
The functionality is extended by allowing users to upload files and also pulling information from a different website using a web scraper.
{{< link-card
  title="Functionality"
  description="Extended functionality including File Upload and Web Scraping"
  href="/docs/website/functionality/"
  target="_blank"
>}}
### 4. Hosting the Website
Finally we will configure a Nginx Server on a Raspberry Pi to serve our site. We will also enable SSL on the Nginx server with a free dynamic domain.
{{< link-card
  title="Hosting"
  description="Self-Hosting the Website on a Raspberry Pi"
  href="/docs/website/hosting/"
  target="_blank"
>}}

---

## 2. eJPT
Once strong foundations are built in the web domain and there is a complete understanding of how websites work. The next step is exposure to security concepts and building a core pentesting methedology. The eJPT is a certification with more than 148-hours of training content and a 48 hour exam which provides real-world pentesting capabilities.

The eJPT introduces the following concepts:
- The phases of a penetration test
- How to approach a target systematically
- How to move from information gathering to testing

The eJPT (eLearnSecurity Junior Penetration Tester) is important for pentesting because it provides structure, fundamentals, and real-world context at the very beginning of a pentester’s journey. Mimicking real-world scenarios and packed with dozens of practical labs, the eJPT builds skills required for hands-on engagements and affirms the individual’s capability to become an asset in any penetration testing team.

The exam is 48 hrs with 35 questions. There are 5–6 machines in DMZ and 1–2 machines in the internal network. You are required to pivot from the DMZ to the internal network and also escalate your priviledges.

### Curriculum
![My photo](/ejptcontent.png)

### Notes:
{{< link-card
  title="Tools"
  description="An overview of tools such as Nmap and Metasploit"
  href="/docs/eJPT/tools/"
  target="_blank"
>}}
{{< link-card
  title="Common Ports"
  description="Services on Common Ports and Attacks against it"
  href="/docs/eJPT/ports/"
  target="_blank"
>}}
{{< link-card
  title="Pivoting"
  description="Establishing a pivot point to move through a network after initial access"
  href="/docs/eJPT/pivoting/"
  target="_blank"
>}}
{{< link-card
  title="Linux Enumeration and Priviledge Escalation"
  description="Information Gathering on the compromised Linux host and increasing priviledges"
  href="/docs/eJPT/linux/"
  target="_blank"
>}}
{{< link-card
  title="Hosting"
  description="Information Gathering on the compromised Windows host and increasing priviledges"
  href="/docs/eJPT/windows/"
  target="_blank"
>}}

---

## 3. eWPT
eWPT is a hands-on, professional-level Red Team certification that simulates skills utilized during real-world engagements. The exam environment presents a scenario of a web application pentests that you need to perform on a collection of end-points. You have 10 hours to test the applications and services found in scope and 50 questions to answer in that time. You will need an overall passing score of 75% or above to pass the exam. The questions consist of multiple choice and short answer questions. These are contextual to the exam environment and may change between exams as it produces dynamic ‘flags’ to collect. Make no mistake, this is not a CTF style exam. You need to perform a pentest to uncover the answers. 

### Curriculum
![My photo](/ewptcontent.png)

### Notes:
{{< link-card
  title="Information Gathering"
  description="An overview of tools such as Nmap and Metasploit"
  href="/docs/eWPT/info/"
  target="_blank"
>}}
{{< link-card
  title="Cross Site Scripting"
  description="Attaching code onto a legitimate website that will execute when the victim loads the website."
  href="/docs/eWPT/xss/"
  target="_blank"
>}}
{{< link-card
  title="SQL Injection"
  description="Code injection technique used to modify or retrieve data from SQL databases"
  href="/docs/eWPT/sqli/"
  target="_blank"
>}}
{{< link-card
  title="Content Management Systems"
  description="Common attacks on CMS systems such as Wordpress and Joomla"
  href="/docs/eWPT/cms/"
  target="_blank"
>}}
{{< link-card
  title="Directory Traversal"
  description="Accessing unauthorized files and directories outside a web application's intended folder."
  href="/docs/eWPT/lfi/"
  target="_blank"
>}}
{{< link-card
  title="Tools"
  description="Exploring tools such as wafwoof and weeveley to automate attacks"
  href="/docs/eWPT/tools/"
  target="_blank"
>}}

---

## 4. BSCP

The Burp Suite Certified Practitioner (BSCP) is an official certification for web security professionals, from the makers of Burp Suite. Becoming a Burp Suite Certified Practitioner demonstrates a deep knowledge of web security vulnerabilities. The certification consist of a collection of 300+ labs. 

### Curriculum
| **Topic Category**              | **Specific Topic**                   | **Approx. Number of Labs**   |
| ------------------------------- | ------------------------------------ | ---------------------------- |
| **Server‑Side Vulnerabilities** | SQL Injection                        | 18 labs                      |
|                                 | Authentication                       | 14 labs                      |
|                                 | Path Traversal (Directory Traversal) | 6 labs   |
|                                 | Command Injection                    | 5 labs   |
|                                 | Business Logic Vulnerabilities       | 11 labs   |
|                                 | Information Disclosure               | 5 labs   |
|                                 | Access Control                       | 13 labs   |
|                                 | File Upload Vulnerabilities          | 7 labs |
|                                 | Race Conditions                      | 6 labs   |
|                                 | Server‑Side Request Forgery (SSRF)   | 7 labs   |
|                                 | XXE Injection                        | 9 labs  |
|                                 | NoSQL Injection                      | 4 labs   |
| **Client‑Side Vulnerabilities** | Cross‑Site Scripting (XSS)           | 30 labs   |
|                                 | Cross‑Site Request Forgery (CSRF)    | 12 labs   |
|                                 | Cross‑Origin Resource Sharing (CORS) | 4 labs  |
|                                 | Clickjacking (UI Redressing)         | 5 labs   |
|                                 | DOM‑Based Vulnerabilities            | 7 labs   |
|                                 | WebSockets                           | 3 labs   |
| **Advanced / Other Topics**     | Insecure Deserialization             | 10 labs  |
|                                 | GraphQL API Vulnerabilities          | 5 labs    |
|                                 | Server‑Side Template Injection       | 7 labs   |
|                                 | Web Cache Poisoning                  | 13 labs  |
|                                 | HTTP Host Header Attacks             | 7 labs   |
|                                 | HTTP Request Smuggling               | 22 labs  |
|                                 | OAuth Authentication                 | 6 labs   |
|                                 | JWT Attacks                          | 8 labs   |
|                                 | Prototype Pollution                  | 10 labs   |
|                                 | Web LLM Attacks                      | 4 labs   |
|                                 | Essential Skills                     | 2 labs  |


### Notes:
{{< link-card
  title="Request Smuggling"
  description="An attack in which the web server and a proxy/load balancer disagree about where one HTTP request ends and the next begins. This lets the attacker “smuggle” a hidden request through the system."
  href="/docs/bscp/request-smuggling/"
  target="_blank"
>}}
{{< link-card
  title="Web Cache Attacks"
  description="Web cache Poisoning - the cache stores a malicious or incorrect response, which is then served to many users. Web Cache Deception - the cache stores private or sensitive content as if it were public."
  href="/docs/bscp/web-cache-attacks/"
  target="_blank"
>}}
{{< link-card
  title="JWT / oAuth Attacks"
  description="Misconfigurations in the configurations of JWT/oAuth expose security vulnerabilities."
  href="/docs/bscp/jwt-/-oauth-attacks/"
  target="_blank"
>}}
{{< link-card
  title="Cross Origin Resource Sharing"
  description="The implementation of CORS may contain mistakes or be overly lenient to ensure that everything works, and this can result in exploitable vulnerabilities."
  href="/docs/bscp/cross-origin-resource-sharing/"
  target="_blank"
>}}
{{< link-card
  title="Prototype Pollution"
  description="It enables attackers to add arbitrary properties to global object prototypes, which may then be inherited by user-defined objects."
  href="/docs/bscp/prototype-pollution/"
  target="_blank"
>}}
{{< link-card
  title="Insecure Deserialization"
  description="Insecure deserialization is when user-controllable data is deserialized by a website."
  href="/docs/bscp/insecure-deeserialization/"
  target="_blank"
>}}