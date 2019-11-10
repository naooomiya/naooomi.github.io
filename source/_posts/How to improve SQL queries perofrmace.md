---
title: How to improve SQL queries performance
date: 2019-11-01 00:39:27
categories: SQL
tags: SQL
---

## 1. Only Retrieve The Data You Need
The mindset of "the more data, the better" isn't the correct way when you're writing SQL query. You SQL performance might suffer from the fact that your query is trying to pull to too much data. So that's why it's generally a good idea to look out for the **SELECT** statement, the **DISTINCT** and **UNION** clause and the **LIKE** operator

<!-- more -->

#### The SELECT Statement
The first thing you can check when you have written your query is whether the **SELECT** statement is as compact as possible. Do not get used to ```select *``` because in the most cases, you don't need that and the unnecessary columns places extra loads on the database which will slown down the single SQL and the system. Besides, it can increase the consumption of extra I/O, memory and CPU as well. It's better for you to specify the columns you want. 


#### The DISTINCT and UNION clause

**DISTINCT** and **UNION** should be used only if it is necessary. **DISTINCT** and **UNION** operators cause sorting, which slows down the SQL execution. 

The ```SELECT DISTINCT``` statement is used to return only distinct(different) values. The execution time only increases if you add this clause to your query. **DISTINCT** works by grouping all fields in the query to create distinct results. To accomplish this goal however, a large amount of processing power is required. 

It's therefore always a good idea to consider whether you need this ```DISTINCT```. 
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

## 4. Create joins with INNER JOIN rather than WHERE
I used to prefer to make joins with **WHERE** clause, such as the following:

```
SELECT dwColumns.ID, dwColumns.Name, dwTables.ID, dwTables.Name
FROM dwTables, dwColumns
WHERE dwTables.ID = dwColumns.tableID
```

This type of join creates a Cartesian Join, also called a Cartesian Product or **CROSS JOIN**. In Cartesian Join, all possible combinations of the variables are creates. In this example, if we had 1,000 tables with 100 columns for each table, the query would first genrate 100,000 results, then filter for the 1,000 records where the table ID is correctly joined. This is an inefficient use of database resources. Cartesian Joins are especially problematic in large-scale databases, because a Cartesian Join of two large tables could create billions or trillions of results. 

To avoid creating a Cartesion Join, **INNER JOIN** should be used instead:

```
SELECT dwTables.ID, dwTables.Name, dwTables.ID, dwTables.Name
FROM dwTables
    INNER JOIN dwColumns
    ON dwTables.ID = dwColumns.tableID
```

## 5. Avoid using wildcard(%) at the beginning of a predicate.

The predicate LIKE '%abc' causes full table scan. 

When a leading wildcard is used, especially in combination with an ending wildcard, the database is tasked with searching all records for a match anywhere within the selected fields. 

For example:

```
SELECT * FROM TABLE1 WHERE COL1 LIKE '%abc'
```
