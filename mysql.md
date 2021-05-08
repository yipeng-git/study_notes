# Introduction

## Basic Manipulation Operations

Manipulate database -> manipulate table in database -> manipulate data in table

### Connect to MySQL database

```
mysql -P <port> -h <address> -u <username> -p<password>
```

### Databases

#### Create Database

```sql
CREATE DATABASE [IF NOT EXISTS] mydatabase;
```

#### Delete Database

```sql
DROP DATABASE [IF EXISTS] mydatabase;
```

#### Show All Databases

```sql
show databases; -- show all databases
```

#### Use Database

```sql
use <database> -- switch to databse
```

### Tables

#### Show Tables

```sql
show tables; -- show all tables
```

#### Show Table Information

```sql
show columns in <table>; -- show all the columns
describe <table>; -- = show columns
show create table <table>; -- show the info using to create the table, including the defination of columns
```



## Database Languages

### Database Define Language (DDL)

### Database Manipulate Language (DML)

### Database Query Language (DQL)

### Database Control Language (DCL)

## Data Types

### Numeric Data Types

#### Integer Types

For integer data types, ***M*** indicates the maximum display width. The maximum display width is 255. 

For floating-point and fixed-point data types, ***M*** is the total number of digits that can be stored.

If you specify `ZEROFILL` for a numeric column, MySQL automatically adds the `UNSIGNED` attribute to the column.

Numeric data types are signed by default.

-   BIT



# InnoDB

## ACID Model

-   A: atomicity 原子性

    If any of the statements constituting a transaction fails to complete, the entire transaction fails and the database is left unchanged.

    Related MySQL features: autommit setting, the `COMMIT` statement, the `ROLLBACK` statement.

-   C: consistency 一致性

    A transaction can only bring the database from one valid state to another, maintaining database invariants. This prevents database corruption by an illegal transaction, but does not guarantee that a transaction is *correct*.

    Related MySQL features: doublewrite buffer, crash recovery.

-   I: isolation 隔离性

    Isolation ensures that concurrent execution of transactions leaves the database in the same state that would have been obtained if the transactions were executed sequentially.

    Related MySQL features: autocommit setting, transaction isolation levels and the `SET TRANSACTION` statement, the low-level details of IInnoDB locking.

-   D: durability 持久性

    Once a transaction has been commited, it will remain committed even in the case of a system failure (power outage or crash).

## Multi-Versioning







