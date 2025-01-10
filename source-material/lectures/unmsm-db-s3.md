---
tags:
  - "#lecture-notes"
src-date: 2024-09-02
src-author:
  - Gustavo Arredondo
src-link: Databases I
---
# Databases I - Session 3

- programmers should get involved in the design of the database
- nowadays, many business rules can be implemented in the DBMS itself

## Filesystems

- concurrency is slow and complicated
- lack of integrity enforcement mechanisms
- poor scalability
- file access policies aren't granular enough
- lots of redundancies
- lack of querying mechanisms

## DBMS

- the database is just the repository
- the DBMS is a *program* that works as an **interface** between the database and its administrators, allowing to store, query, and manipulate data in a safe and efficient manner

![Pasted image 20240902134845](../../utilities/attachments/Pasted%20image%2020240902134845.png)

- they implement [SQL](SQL) as a means to query data
- controls who can access certain elements and how
- ensures data integrity
	- example: when deleting a register from a certain table, the DBMS deletes every other register that references it
- allows grouping operations as [transactions](database%20transactions) that either finish executing entirely or don't execute at all (ACID)
- allows to roll back accidental changes
- uses indices, among other techniques, to optimize queries
- allows audits and system monitoring

## Normalization techniques

- [Normalization](database%20normalization) is about organizing data in certain ways in order to
	- control redundancy
	- optimize queries
	- improve integrity
- Functional dependency
	- Transitive dependency

### First normal form

- All attributes are indivisible, no field has multiple values


![Pasted image 20240902153058](../../utilities/attachments/Pasted%20image%2020240902153058.png)

### Second normal form

- All non-key attributes depend on the table's primary key
- In other words, every attribute in a table must describe the table's entity

### Third normal form

- No transitive dependencies

### Fourth normal form

- No multi-value dependencies

### Boyce-Codd normal form

