---
title: AWS Service | RDS(Relational Database Service) 101
date: 2020-01-12 23:08:13
tags:
    - [AWS Services]
    - [Relational Database Service]
    - [RDS]
    - [AWS Certified Developer - Associate]
categories:
    - [AWS Services]
    - [Relational Database Service]
    - [AWS Certified Developer - Associate]
---


### 1. What is a relational Database?
Relational Databases are what most of us are all used to. They have been around since the 70s. Think of a traditional spreadsheet:
- Database
- Tables
- Row
- Fields(Columns)

<!-- more -->

### 2. Relational Database Types
- SQL Server
- Oracle
- MySQL Server
- PostgreSQL
- Aurora
- MariaDB

### 3. Non Relational Database
- Database
	- Collection (= Table)
	- Document (= Row)
	- Key Value Pairs (= Fields)
- No pre-define table structure

### 4. What is Data Warehousing?
A **Data Warehousing (DW)** is process for collecting and managing data from varied sources to provide meaningful business insights. A Data Warehouse is typically used to connect and analyse business data from heterogeneous sources. 
	
### 5. OLTP vs OLAP
**Online Transaction Processing (OLTP)** differs from OLAP **Online Analytics Processing (OLAP)** in terms of the types of queries you will run. OLTP is an online data modification system while OLAP is an online historical multidimensional data retrieval system, which retrieves the data for analysis that can help in decision making. Which one to use depend upon the users requirement for both works for different purpose. 
	
#### Definition of OLTP
OLTP is an **Online Transaction Processing System**. The main focus of OLTP system is to record the current **Update**, **Insertion** and **Deletion** while transaction. The OLTP queries are **simpler** and **short** and hence require **less time in processing**, and also requires **less space**. 

OLTP database gets **updated frequently**. It may happen that a transaction in OLTP fails in middle, which may effect data integrity. So, it has to take special care of **data integrity**. OLTP database has **normalized tables (3NF)**.
	
The best example for OLTP system is an **ATM**, in which using short transactions we modify the status of our account. OLTP system becomes the source of data for OLAP. 
	
#### Definition of OLAP
OLAP is an **Online Analytical Processing system**. OLAP database stores historical data that has been inputted by OLTP. It allows a user to view different summaries of multi-dimensional data. Using OLAP, you can extract information from a large database and analyse it for decision making. 

OLAP also allow a user to execute **complex queries** to extract multidimensional data. In OLTP system to retrieve data from a large database to analyse. Simply the user can fire the query again and extract the data for analysis. 
	
The transaction in OLAP are **long** and hence take comparatively **more time** for processing and requires large space. The transactions in OLAP are **less frequent** as compared to OLTP. Even the tables in OLAP database may not be normalized. The example for OLAP is to view a financial report, or budgeting, marketing management, sales report, etc. 
	
	
| Comparison | OLTP |	OLAP |
|:----------:|:----:|:------:|
| Basic | It is an online transactional system and manages database modification | It is and online data retrieving and data analysis system. |
| Focus | Insert, Update, Delete information from the database | Extract data for analysing that helps in decision making |
| Data | OLTP and its transactions are the original source of data | Different OLTPs database becomes the source of data for OLAP |
| Transaction | OLTP has short transactions	| OLAP has long transactions |
| Time | The processing time of a transaction is comparatively less in OLTP | The processing time of a transaction is comparatively more in OLAP |
| Queries | Simpler queries | Complex queries |
| Normalization | Tables in OLTP database are normalized(3NF) | Tables in OLAP database are not normalized |
| Integrity | OLTP database must maintain data integrity constraint | OLAP database does not get frequently modified. Hence, data integrity is not affected. | 
	
### 6. What is Elasticache?
ElasticCache is a web service that makes it easy to deploy, operate, and scale an in-memory cache in the cloud. The service improves the performance of web applications by allowing you to retrieve information from fast, managed, in-memory caches, instead of replying entirely on slower disk-based databases.
	
ElasticCache supports two open-source in-memory caching engines:
- Memcached
- Redis
		
### 7. Summary
- RDS - OLTP
	- SQL
	- MySQL
	- PostgreSQL
	- Oracle
	- Aurora
	- MariaDB
- DynamoDB - No SQL
- RedShift - OLAP
- Elasticache - In Memory Caching:
- Memcached
- Redis

	
	
	
	


