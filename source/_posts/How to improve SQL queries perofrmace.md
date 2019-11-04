---
title: How to improve SQL queries performance
date: 2019-11-01 00:39:27
categories: SQL
tags: SQL
---

# How to improve SQL queries performance

## 1. Only Retrieve The Data You Need
The mindset of "the more data, the better" isn't the correct way when you're writing SQL query. You SQL performance might suffer from the fact that your query is trying to pull to too much data. So that's why it's generally a good idea to look out for the **SELECT** statement, the **DISTINCT** and **UNION** clause and the **LIKE** operator

<!-- more -->

#### The SELECT Statement
The first thing you can check when you have written your query is whether the **SELECT** statement is as compact as possible. Do not get used to ```select *``` because in the most cases, you don't need that and the unnecessary columns places extra loads on the database which will slown down the single SQL and the system. Besides, it can increase the consumption of extra I/O, memory and CPU as well. It's better for you to specify the columns you want. 


#### The DISTINCT and UNION clause
**DISTINCT** and **UNION** should be used only if it is necessary. 
**DISTINCT** and **UNION** operators cause sorting, which slows down the SQL execution. 
The ```SELECT DISTINCT``` statement is used to retunr only distinct(different) values. The execution time only increases if you add this clause to your query. It's therefore always a good idea to consider whether you need this ```DISTINCT```. 
Use **UNION ALL** instead of **UNION**, if possible, as it is much more efficient.  


#### The LIKE operator
The predicate **LIKE** ````'%abc'```` causes a full table scan. So try to avoid using wildcard(%) at the beginning of a predicate. 

## 2. Limit Your Results
- You can add ```LIMIT``` or ```TOP``` clauses to your query to set a maximum number of rows for the result set. 
- Additionally, you can also add the ```ROWNUM```clause, which is equivalent to using ```LIMIT```in your query. See the examples below. 

```
SELECT * FROM Users
WHERE age = 25 AND ROWNUM <= 5;

SELECT * FROM Users LIMIT 5
WHERE age = 25 AND;
```

## 3. Don't Make Queries More Complex Than They Need To Be
Try to keep your query simple and efficient



##  4. Unitied SQL Query
I believe some developers think these two queries are the same(at least I believe before writing this blog). But actually 
