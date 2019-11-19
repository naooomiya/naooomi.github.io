---
title: SQL Commands
date: 2019-11-19 17:19:31
tags:
categories: SQL
---

Structured Query Language(SQL) as we all know is the database language by the use of wich we can perform certain operations on the existing database and also we can use this language to create a database. SQL uses certain commands like Create, Drop, Insert stc. to carry out the required tasks. 

<!-- more -->

These SQL commands are mainly categorized into four categories as:
1. DDL - Data Definition Language
2. DQL - Data Query Language
3. DML - Data Manipulation Language
4. DCL - Data Control Language

Though many resources claim there to be another category of SQL clauses TCL - Transaction Control Language.

![Types of SQL Commands](https://i.imgur.com/uZg5Qre.png)

### 1. DDL(Data Definition Language): 
DDL or Data Definition Language actually consists of the SQL commands that can be used to define the database schema. It simpy deals with descriptions of the database schema and is used to create and modify the structure of database objects in the database.
	
**Examples of DDL commands:**
- CREATE - is used to create the database or its objects (like table, index, function, views, store procedure and triggers)
- DROP - is used to delete objects from the database
- ALTER - is used to alter the structure of the database
- TRANCATE - is used to remove all records from a table, including all spaces allocated for the records are removed
- COMMENT - is used to add comments to the data dictionary
- RENAME - is used to rename an object existing in the database

### 2. DQL (Data Query Language):
DQL statements are used for performing queries on the data within schema objects. The purpose of DQL Command is to get some schema relation based on the query passed to it.

**Eample of DQL:**
- SELECT - is used to retrieve data from the database

###	3. DML(Data Manipulation Language):
The SQL commands that deals with the manipulation of data present in the database belong to DML or Data Manipulation Language and this includes most of the SQL statements.
	
**Eamples of DML:**
- INSERT - is used to insert data into a table
- UPDATE - is used to update existing data within a table
- DELETE - is used to delete records from a database table
	
###	4. DCL(Data Control Language):
DCL included commands such as GRANT and REVOKE which mainly deals with the rights, permissions and other controls of the database system.
	
**Examples:**
- GRANT - gives user's access privileges to database
- REVOKE - withdraw user's access privileges given by using the GRANT command
	
###	5. TCC(Transaction Control Commands):TCL commands deals with the transaction within the database.

**Examples of TCL commands:**
- COMMIT - commits a transaction
- ROLLBACK - rollbacks a transaction in case of anu error occurs
- SAVEPOINT - set a savepoint within a transaction
- SET TRANSACTION - specify characteristics for the transaction
