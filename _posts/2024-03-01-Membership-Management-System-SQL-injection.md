---
title: Membership Management System - SQL injection
published: true
---

- Title: Membership Management System - SQL injection
- Application: Membership Management System
- Date: 01.03.2024
- Bugs: SQL injection
- Exploit Author: SoSPiro
- Vendor Homepage: https://codeastro.com/author/nbadmin/
- Software Link: https://codeastro.com/membership-management-system-in-php-with-source-code/
- Version: 1.0
- Tested on: Windows 10 64 bit Wampserver

### Vulnerability Description:

The provided payload in the POST request indicates a potential SQL injection vulnerability. Specifically, the manipulation within the email and password parameters suggests an attempt to influence the SQL query directly, presenting a risk for exploiting security vulnerabilities.

### SQL Injection:

This manipulated submission aims to affect the SQL query by incorporating user input. For instance, the use of **sleep(5)** introduces a time-delay technique, indicative of a potential resource-consuming attack vector by malevolent actors.


### Vulnerability Details:
- **Application Name**: Membership Management System
- **Software Link**: [Download Link](https://codeastro.com/membership-management-system-in-php-with-source-code/)
- **Vendor Homepage**: [Vendor Homepage](https://codeastro.com/author/nbadmin/)

### The vulnerability lies in the following code snippet:

```php
$email = $_POST['email'];
$password = $_POST['password'];

$hashed_password = md5($password);
$sql = "SELECT * FROM users WHERE email = '$email' AND password = '$hashed_password'";
```

The provided PHP code section exacerbates the SQL injection risk by directly incorporating user input into the SQL query. To mitigate this vulnerability, the use of parameterized queries or prepared statements is recommended.


### Proof of Concept (PoC):

- first we build the project and come to index.php

- We write and send the payload to the email and password parts.

- Below is an example payload illustrating the SQL injection vulnerability:
```
email=test@123.asd' + (SELECT * FROM (SELECT (SLEEP(5)))a) +'&password=admin' or '1'='1'&login=
```

In this example, the **sleep(5)** function is employed to induce a time delay, followed by the use of or **'1'='1'** in the password control section, aiming to always evaluate as true.

- Request Response
![asd](https://gcdnb.pbrd.co/images/9k8xy4YRomp3.png?o=1)
