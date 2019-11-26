---
title: Database Normalization Explained
date: 2019-11-26 19:54:15
tags: 
    - [Database Normalization]
    - [SQL]
    - [1NF]
    - [2NF]
    - [3NF]
categories:
    - [SQL]
    - [Database]
---

**Normalization** is a database design technique which organizes tables in a manner that avoids data redundancy, insertion anomaly, update anomaly and deletion anomaly.

<!-- more -->

## Anomalies in DBMS
There are three types of anomalies that occur when the database is not normalized. These are **Insertion**, **Update** and **Deletion** anomaly. 

**Example :**

Suppose a manufacturing company stores the employee details in a table named employee that has four attributes: emp_id for storing employee's id, emp_name for storing employee's name, emp_address for storing employee's address and emp_dept for storing the department details in which the employee works. At some point of time the table looks like this: 

| emp_id	| emp_name	| emp_address	| emp_dept |
|:---------:|:---------:|:-------------:|:--------:|
| 101	    | Rick	    | AddressA	    | D001     |
| 101	    | Rick      | AddressA	    | D002     |
| 123	    | Maggie	| AddressB	    | D890     |
| 166	    | Glenn	    | AddressC	    | D900     |
| 166	    | Glenn     | AddressC	    | D004     |

The above table is not normalized. Here are the problems we could face when a table is not normalized.
*    **Update anomaly**

    In the above table we have two rows for employee Rick as he belongs to two departments of the company. If we want to update the address of Rick then we have to update the same in two rows or the data will become inconsistent. If somehow, the correct address gets updated in one department but not in other then as per the database, Rick would be having two different addresses, which is not correct and would lead to inconsistent data. 

+    **Insert anomaly**

    Suppose a new employee joins the company, who is under training and currently not assigned to any department then we would not be able to insert the data into the table if emp_dept field doesn't allow nulls.

-    **Delete anomaly**

    Suppose, if at a point of time the company closes the department D890 then deleting the rows that are having emp_dept as D890 would also delete the information of employee Maggie since she is assigned only to this department.  

---

## Database Normal Forms

### 1NF(First Normal Form) Rules

* A column of a table cannot hold multiple values. Each table cell should contain a single value (atomic value)
* Each record needs to be unique

This is one table that is without normalization because the Movies and Category columns have multiple values :

| Name	 | Address	          | Movies                       	 | Salutation | Category         |
|:------:|:------------------:|:--------------------------------:|:----------:|:----------------:|
| Janet	 | Flat B, 6th Street |	Deadpool, Spider-Man             | Ms.	      | Action, Action   |
| Robert | 3rd Street	      | Call Me by Your Name, La La Land | Mr.	      | Romance, Romance |
| Robert | 5th Avenue	      | Spider-Man                   	 | Mr.	      | Action           |

(Table 0)

The above table in **1NF** will look like this : 

#### 1NF Example: 

| Name	 | Address            | Movies Rented	     | Salutation | Category |
|:------:|:------------------:|:--------------------:|:----------:|:--------:|
| Janet  | Flat B, 6th Street | Deadpool             | Ms.        | Action   |
| Janet	 | Flat B, 6th Street | Spider-Man           | Ms.        | Action   |
| Robert | 3rd Street         | Call Me by Your Name | Mr.        | Romance  |
| Robert | 3rd Street         | La La Land           | Mr.        | Romance  |
| Robert | 5th Avenue         | Spider-Man           | Mr.        | Action   |

(Table 1: In 1NF)

A few things too understand first:

#### What is a KEY?
A **KEY** is a value used to identify a record in a table uniquely. A **KEY** could be a single column or combination of multiple columns.

Note: Columns in a table that are NOT used to identify a record uniquely are called non-key columns

#### What is a primary Key?
A primary is a single column value used to identify a database record uniquely.

It has following attributes
- A primary key cannot be **NULL**
- A primary key value must be **unique**
- The primary key values should rarely be changed
- The primary key must be given a value when a new record is inserted

#### What is a Composite Key?
A **composite key** is a primary key composed of multiple columns used to identify a record uniquely

Take the above table as an example, the Name column is not unique. Hence, we require both Name and Address to identify a record uniquely. That is a **composite key**. 

Now, move to **Second Normal Form (2NF)**

### 2NF(Second Normal Form) Rules

- Rule 1 - Follow 1NF
- Rule 2 - **Single Column Primary Key**

It's clear that we cannot move forward to make simple database in 2nd Normalization form unless we partition the table above. 

#### 2NF Example: 

| Membership ID | Name   | Physical Address   | Salutation |
|:-------------:|:------:|:------------------:|:----------:|
| 1             | Janet	 | Flat B, 6th Street | Ms.        |
| 2             | Robert | 3rd Street         | Mr.        |
| 3             | Robert | 5th Avenue         | Mr.        |

(Table 1)

|Membership ID | Movies Rented        |
|:------------:|:--------------------:|
| 1	           | Deadpool             |
| 1	           | Spider-Man           |
| 2            | Call Me by Your Name |
| 2	           | La La Land           |
| 3	           | Spider-Man           |

(Table 2)

We have divided our 1NF table into two tables, Table 1 and Table 2. Table 1 contains member information. Table 2 contains information on movies rented. 

We have introduced a new column called **Membership_ID** which is the primary key for Table 1. Records can be uniquely identified in Table 1 using membership id. 

#### Database - Foreign Key
In Table 2, Membership ID is the **Foreign Key**:

Foreign Key references the primary key of another Table! It helps connect your tables
- A foreign key can have a different name from its primary key
- It ensures rows in one table have corresponding rows in another
- Unlike the Primary Key, they do not have to be unique. Most often they aren't
- Foreign keys can be null even though primary keys can not

| Membership ID	| Movies Rented         |
|:-------------:|:---------------------:|
| 1             | Deadpool              |
| 1	            | Spider-Man            |
| 2	            | Call Me by Your Name  |
| 2	            | La La Land            |
| 3	            | Spider-Man            |

(Table 2)

  - Foreign Key references Primary Key
  - Foreign Key can only have values present in primary key
  - It could have a name other than that of Primary Key

| Membership ID | Name   | Physical Address   | Salutation |
|:-------------:|:------:|:------------------:|:----------:|
| 1             | Janet	 | Flat B, 6th Street |	Ms.        |
| 2	            | Robert | 3rd Street         | Mr.        |
| 3	            | Robert | 5th Avenue         | Mr.        |

(Table 1)

#### Why need a foreign key?

You will only be able to insert values into your foreign key that exist in the unique key in the parent table. That helps in referential integrity

1. Insert a record in Table 2 where Membership ID = 101
	
    | Membership ID	| Movies Rented      |
    |:-------------:|:------------------:|
    | 101           | Mission Impossible |

2. But Membership ID 101 is not present in Table 1
	
    | Membership ID | Name   | Physical Address   |	Salutation |
    |:-------------:|:------:|:------------------:|:----------:|
    | 1	            | Janet  |	FlatB, 6th Street |	Ms.        |
    | 2	            | Robert |	3rd Street        | Mr.        |
    | 3	            | Robert |	5th Avenue        | Mr.        |
    
    (Table 1)
	
3. Database will throw an ERROR. This helps in **referential integrity**

The above problem can be overcome by declaring membership ID from Table 2 as foreign key of membership ID from Table 1

Now, if somebody tries insert a value in the Membership ID field that does not exist in the parent table, an error will be shown.

#### What are transitive functional dependencies?
A **transitive function dependency** is when changing a non-key column, might cause any of the other non-key columns to change

Consider the table 1. Changing the non-key column Name may change Salutation

| Membership ID | Name   | Physical Address   |	Salutation |
|:-------------:|:------:|:------------------:|:----------:|
| 1             | Janet  | Flat B, 6th Street |	Ms.        |
| 2	            | Robert | 3rd Street	      | Mr.        |
| 3	            | Robert | 5th Avenue	      | Mr.        |

(Table 1)

Let's move into **3NF**

### 3NF(Third Normal Form) Rules
- Rule 1 - Follow 2NF
- Rule 2 - Has **no transitive functional dependencies**

To move 2NF table into 3NF, we again need to divide the table

#### 3NF Example:

| Membership ID | Name   | Physical Address   | Salutation ID | 
|:-------------:|:------:|:------------------:|:-------------:|
| 1             | Janet	 | Flat B, 6th Street |	2             |
| 2	            | Robert | 3rd Street         | 1             |
| 3	            | Robert | 5th Avenue         | 1             |

(Table 1)

| Membership ID | Movies Rented        |
|:-------------:|:--------------------:|
| 1	            | Deadpool             |
| 1	            | Spider-Man           |
| 2	            | Call Me by Your Name |
| 2	            | La La Land           |
| 3	            | Spider-Man           |

(Table 2)

| Salutation ID | Salutation |
|:-------------:|:----------:|
| 1             | Mr.        |
| 2             | Ms.        |
| 3	            | Mrs.       |
| 4	            | Dr.        |

(Table 3)


We have again divided our tables and created a new table which stores Salutations. There are no transitive functional dependencies, and hence our table is in 3NF. In Table 3 Salutation ID is primary key, and in Table 1 Salutation ID is the foreign to primary key in Table 3. 

Now our little example is at a level that cannot further be **decomposed** to attain higher forms of normalization. Infact, it is already in higher normalization forms. Separate efforts for moving into next levels of normalizing data are normally needed in complex databases.

### Boyce-Codd Normal Form(BCNF)
Even when a database is in 3rd Normal Form, still there would be anomalies resulted if it has more than one Candidate Key.

Sometimes BCNF is also referred as 3.5 Normal Form.

### 4NF(Fourth Normal Form) Rules
If no database table instance contains two or more, independent and multivalued data describing the relevant entity, then it is in 4th NF.

### 5NF(Fifth Normal Form) Rules
A table is in 5th Normal Form only if it is in 4NF and it cannot be decomposed into any number of smaller tables without loss of data.

### 6NF(Sixth Normal Form) Rules
Normally, it wouldn't be used. 


## Summary
- Database designing is critical to the successful implementation of a database management system that meets the data requirements of an enterprise system
- Normalization helps produce database systems that are cost-effective and have better security modles
- Functional dependencies are a very important component of the normalize data process
- Most database systems are normalized database up to the third normal forms
- A primary key uniquely identifies record in a Table and cannot be null
- A foreign key helps connect table and references a primary key

