
# Relational Databases 

A type of structure database in which data is stored following a tabular format (tabular-like structure); often supports powerful querying using SQL. In toher words, it's going to be store in the form of tables. Tables are also called relations in a relational database. These tables follows a special schema, with a specific data type on each column.

## Non-Relational Database

In contrast with relational database (SQL database), a type of database that is free of imposed, tabular-like structure (They don't imposed this tabular data format). Non-relational database are often referred as to as NoSQL databases.

## SQL

Structure Query Language. Relational databases can be used using a derivate of SQL such as PostgreSQL in the case of Postgress.
Is effectly a programming language for database. It is used to perform complex queries in relational databases and perform data operations in a very efficient way.

Most relational database supports SQL, but not all of them. 

## SQL Database

Any database that supports SQL. This term is often used synonymosly with "Relational Database", though in practice, not every relational database supports SQL.
## NoSQL Database

Any database that is not SQL compatible is called NoSQL.

## ACID Transaction

A type of database transaction that has four important properties:

1. **Atomicity**: The operations that construct the transaction will either **all** succeed or **all** fail. There is no in-between state. If for some reason one fails because of lost networking, all will fail.
2. **Consistency**: The transaction cannot bring the database to an invalid state. After the transaction is commited or rolled back, the rules for each record will still apply, and all future transactions will see the effect of the past transactions. ALso named Strong Consistency.
3. **Isolation**: The execution of multiple transaction concurrently (at the same time) will have the same effect as if they have been executed sequentially. Remember Clements example, when you begin a transaction twice (from two terminals), one will be in a waiting mode till the other when will commit.
4. **Durability**: Any commited transaction is written to non-volatile storage. It will not be undone by a crash, powr loss, or network partition.

Remember Begin, Commit and Rollback

## Databse Index

A special auxiliarity data structure that allows your database to perform certain queries much faster. Indexes can typically only exist to reference structured data, like data stored in relational database. In practice you create an index on one or multple columns in your database to greatly speed up read queries that you run very often, with the downside of slightly longer writes to your database, since writes have to also take place in the relevant index because the datatype is more complex.

## Strong Consistency

Strong Consistency usually refers to the consistency of ACID transactions, as opposed to Eventual Consistency.

## Eventual Consistency

A consistency model which is unlikly Strong Consistency. In this model, reads might return a view of the system that is stale (old). An ventually consistency datastore will give guarantees that the sate of the database will eventually reflect writes within a time period (could be 10 seconds, or minute).

## Postgress

A relational database that use a dialect of SQL called [PostgreSQL](https://postgresql.org). Provides ACID transactions.

