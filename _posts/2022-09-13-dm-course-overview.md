---
title: CSCI 381 - Data Modeling Course Overview
author: adrian
date: 2022-09-13 23:12:00 -400
categories: [Databases]
tags: [Course]
pin: false
math: true
mermaid: true
image:
  path: /dm/logo.png
  width: 800
  height: 500
  alt: 
---

# Course Overview - Building Block Approach

* Based upon SQL Server 2019
* Object Oriented styles for object naming convention
  * `PascalCase` - first character capitalized
  * `camelCase` - first character lowercase

`This is the standard in OO and NOSQL(JSON)`

* Oracle Database 12.2 supports 128 character naming length per object(max 30 length prior)
* Schema names or ownership of objects within relational model
* ERD techniques that parallel UML Class Diagrams and OOP design
* Simple domains(user defined datatypes)
* GDPR(EU General Data Privacy Regulation). Dynamic Data Masking techniques
* **Taxonomy** - categorization or classification
  * website's taxonomy is the way data is organized -> **sitemap**
* Stakeholders - top level upper management, head of departments
* Joint Application Development(JAD) - methodology that involves the client or end user in the design and development of an application, through a succession of collaborative workshops called JAD sessions
* ERwin allows to manage large maps through segmentation into smaller and very concise manageable guides(subject areas)
* `Refactoring out information from entities` -> Payment : 3 different types of payment

### Three types of data models
`Conceptual, Logical, Physical` - Portability from conceptual and logical models to **PDMs**

### Entity
* container with a name `singular noun`
* defines the contents of the objects within
* unique (account, person, order)

### Relationship
* relates(connects) entities in **pairs**
* pairs entities as "Parent/Child"
* describes how entities are related using verb phrases
* unique object
  * Customer P has many Orders C
  * Orders C may have only one Customer P

### Attribute @ the **LDM Logical level**
* individual characteristic that is attributed to uniquely defining the specifics of the entity
* stored within the entity container
* unique object (`singular noun`)
  * Person(**Person Id**, Last Name, First Name, Date Of Birth)
  * Account(**Account Id**, Account Type, Social Security Number)

### Fully Qualified Table in the **Physical PDM** - Schema Name and Table

* Schema is a unique object created in a taxonomy which categorizes a group of objects under the schema(**encapsulation**)
  * analogous to namespaces in programming languages

* Table is a physical container with a name that is a singular noun.
  * Entity name shown in `PascalCase` on the PDM
  * definition of the contents of the objects within
  * unique object

Fully Qualified tables

`HumanResources.Employee  ,  Sales.[Order],  Production.Product` 

### Column in **Physical PDM**

* Column is the **physical** implementation of the Attribute(LDM)
* individual characteristic attributed to uniquely define a specific entity into a table
* stored within table container, unique

`Publication.Book`
* Table name - Book
* Schema - Publication
* Fully Qualified Table Name - Publication.Schema

### Sample Data Gathering

`Developing a data model is an iterative process of assessing and reassessing the interactions or relationships between these groups`

### Knowing how to communicate with a diverse group of Stakeholders

* Data modeler needs to work with diverse individuals from various departments with a broad range of skills in either technology and/or the business

`Conceptual`
* for the businessperson
* **goaa is to communicate core business concepts and their definitions.** High altitude view of an organization's data assets
* broad view containing only basic and critical concepts for a given scope, typically fits on a single paper

`Logical`
* **detailed business solution**
* *Business Requirements* **without complicating the model with implementation concerns such as software and hardware**
* LDM details(more objects and attributes) > CDM

`Physical`
* typically a db administrator or technical database professional
* **instantiation** of LDM
* detailed technollogy **with implementation concerns such as the target database software and hardware**

