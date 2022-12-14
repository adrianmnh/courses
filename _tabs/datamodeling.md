---
title: Data Modeling
icon: fa-solid fa-database
order: 3
---

# **CSCI 381 - Data Modeling and Advanced Database Systems**

**Prof. Peter Heller**
---
What is a fully qualified object in MYSQL?

- No concept of ownership in MySQL, thus table names are in the `User.TableName` format
- CamelCase

- GDPR : European Union General Data Protection Regulation(applies to global companies)

- Dynamic Data masking : Hiding information based upon provildge. Supported by most ANSCI SQL databases

<img src="/break.png">

> Individual classes @ home
{: .prompt-tip }



## class 3

MySQL Syntax

Convert article to Pascal Case

## Getting started with MySQL using Docker

Use DBeaver as IDE

```sql
CREATE DATABASE IF NOT EXISTS travel;
```

<img src="/dm/03-01.png">

varchar - UTF-8

## Getting started with MySQL

<img src="/dm/03-02.png">

Retrieving data is also much the same as other relational databases

For instance, the following SELECT statement returns all of the table's data

<img src="/dm/03-03.png">

Inserting multiple rows of data into a MySQL table

<img src="/dm/03-04.png">

This query is binary, either all inserts succeed or none do.

<img src="/dm/03-05.png">

Recreating the travel database. Add tables **manufacturers** and **airplanes**

<img src="/dm/03-06.png">

**snake case** seen above

**pasacal case**:
* 1st letter of everyword is uppercase

Inserting into the two tables

<img src="/dm/03-06.png">

<img src="/dm/03-07.png">

<img src="/dm/03-08.png">

<img src="/dm/03-09.png">

<img src="/dm/03-10.png">

<img src="/dm/03-11.png">

<img src="/dm/03-12.png">

## Stored Procedures

<img src="/dm/03-13.png">

Would this work in SQL Server? **No, we use EXEC in SQL Server**

<img src="/dm/03-14.png">

### Working with parameters

<img src="/dm/03-15.png">

### What is **deterministic**?

<img src="/dm/03-16.png">


# class 4

# Course Overview - Building Block Approach

entity, descriptions, relationships

`physical data model` - specific technologies while logicai]l data model is tech agnostic

conceptual data model - super class entities can derive

Identifying vs non identifying relationships - super class primary key is part of the primary key of the derived entity table
* solid lines - identifying relationships
* segmented lines - non identifying

`PDM` - represents detailed technology with implementation concerns

`tablename postfix id` to use as primary keys for erwin physical data model tables

---


# class 6

## SDLC System development life cycle

## MDLC Model development life cycle 

Difference between a course and a class

Think of a `course` as a superclass, and a `class` is an instantiation of the class

## Objective of Normalization


## Database Anomalies

## Dependencies

**take notes on non identifying relationshipts PAGE 24**

---

## Validations in erwinDM



---

## Keys

identifying relationships, strong standing tables, 

`Look at MongoDB NO SQL database image`


# Identifying(Relationships to tables with foreign keys from self standing entity tables) vs Non Identifying relationships



# class 7


## Notes

**Identifying Relationship** - a portion of Child Table Primary Key is a Foreign Key 

**Non Identifying Relationship** - A Table contains some identifying key, that can be used to identify an outside entity, this key however, **is not** part of the primary key

```
Vehicle ID (PK)
---------------
Make
Year
....
Manufacturer ID ()

```

