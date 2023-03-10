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
Table: Vehicle

   Vehicle ID (PK)
 ---------------------
| Make                |
| Year                | - - - - - - - - - > 
| ManufacturerID (FK) |
| VinNumber (FK)      |
 ---------------------

 Both ManufacturerID and VinNumber are foreign keys
```

<img src="/break.png">

# class 8



# makeupclass 1

## Entity Data Sleuthing

# make up class 2

Attributes Data Sleuthing

Entity

plural entities:
1. being, existence
2. the existence of a thing is contrasted with its attributes


varchar ansci standrad, takes 2bytes ber char
varchar(1) ~ 3 bytes

structure ready to be populated -> forward engineering


# class 8

SQL SERVER -
* DML - Data M Language
* DDL - Data Definition Language

Domains - User Defined Data Types

What ANSI standrad Object describes the Black box?

what's ANSI SQL? A standard for the language, inheritable

BlackBox is a fully quailified domain

Aliasing SQL DAtatypes simulates a unique, strongly typed class name

MySQL does not support the concept of ownership(Schemas) and domains

The domain is the `core foundation` of designing the database

The domain 
* provides for total reuse by encapsulating applocation attributes within an ontology
* is a base reusable object that should be solely used to define attributes
* is strongly typed by a unique association with a SQL Datatype

<img src="/dm/08-01.png">

# makeup class 3


# class 10

every column has a user defined data type

Udt.[DomainName]

SQL server

```sql
SELECT FullyQualifiedTableName, SchemaName, TableName, ColumnName, OrdinalPosotion
FROM Utils.uvw_FindColumnDefinitionPlusDefaultAndCheckConstraint AS u
WHERE (DataType = 'nvarchat(15)')
WHERE (DomainName = 'Country')
ORDER BY Column Name
```

Data Standard can be imported using complete compare.

The target is the right Model, we can import from the Left.

Naming Standards can be used to abbreviate entities

