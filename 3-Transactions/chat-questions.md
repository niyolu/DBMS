# Lab 3 Questions

## What is a transaction? Give an example.

A transaction is at least one or more SQL statements that are grouped togehter as a single unit. You can also name it as **Unit of Work**. A transaction starts with a SQL statement and ends with a **commit**(=makes changes permanent) or **rollback**(=reverses statements)

    connect to MY_DB
    create TABLE_DEPT(DEPT_ID INTEGER NOT NULL, DEPT_NAME VARCHAR(20))
    insert into DEPT values(100, 'Payroll')
    insert into DEPT values(200, 'ACCOUNTING')
    commit
    insert into DEPT values(300, 'SALES')
    rollback
    insert into DEPT values(500, 'MARKETING')
    commit

## Name the ACID-Rules for a transaction. Give definitions.

ACID-rules gurantee that database transactions are processed in a reliable way.
ACID stands for Atomacity, Consistency, Isolation and Durability

        [Atomicity]
        - All statements in the transaction are treated as a unit
        - When the transaction is completed successfully, everything is commited
        - If the transaction fails, everything done up to the point of failure is rolled back

        [Consistency]
        - Any transaction will take the data from one consistent to another, so only valid consistent data
          is stored in the database

        [Isolation]
        - Concurrenct transactions can't interfere with each other

        [Durability]
        - Committed transactions have their changes persisted in the database

## What does concurrency mean in general? Give definitions

Concurrency means to perform transactions in a multi-user environment simultaniously. This allows that several applications work at the same time on the same database, while keeping the data consistent/valid.

## Give the two basic types of locks

- Share locks (S lock)

  acquire when an application wants to read and prevent others from updating the same row

- Exclusive locks (X locks)

  acquire when an aplication updates, inserts or deletes a row

## Problems which can happen if there is no concurrency control

You will be confrontet with four differen problems, whe not using any concurrency control

        [Lost update]
        -> A transaction is overwritten by another user's interaction after the first commit, the overwriting transaction doesn't notice

        [Uncommitted read/"dirty read"]
        -> A transaction reads data that has not been committed

        [Non-repeatable read]
        -> A transaction reads data twice with another transaction modifying it leading to different results on the same data

        [Phantom read]
        -> When a transaction searches while another inserts data with the same search properties a subsequent search will get additional data

## Give an example for lost update, uncommitted read/dirty read, non-repeatable read, phantom read

        [Lost update]
        1. Transaction 1 changes a row of data;
        2. Transaction 2 changes the same row of data;
        3. Transaction 1 commits the update;
        4. Transaction 2 commits the update;

        [Uncommitted read/Dirty Read]
        1. Transaction 1 changes a row of data;
        2. Transaction 2 reads the uncommitted data;
        3. Transaction 1 rolls back;

        [Nonrepeatable Read]
        1. Transaction 1 reads a row of data;
        2. Transaction 2 changes the row of data and commits;
        3. Transaction 1 reads the row of data again and gets different values

        [Phantom read]
        1. Transaction 1 reads a set of rows that satisfy some search criteria;
        2. Transaction 2 inserts a new row that matches transaction 1 's search criteria
        3. If Transaction 1 will re-execute the query that produced the original set of rows,
           a different set of rows will be retrieved

## Name the different levels of protection to isolate data

An isolation level determines how data used in one transaction is locked or isolated from other transactions while it is being accessed. Four different isolation levels are available with db2 (Db2/Ansi - levelname):

        [Repeatable Read/Serializable]
        All rows retrieved by a single transaction are locked.
        Transactions are completely isolated and phantom rows are not seen.

        [Read Stability/Repeatable Read]
        All rows retrieved by a single transaction are locked; transactions are not completely isolated and phantom rows can be seen and nonrepeatable reads can occor, because is doesn't completely isolate one transaction from the effects of other concurrent transactions.

        [Cursor Stability/Read Commited]
        Any row beeing accessed by a transaction is locked, provided the cursor is positioned on that row. transactions running under the Cursur stability level can't see uncommitted changes made by other transactions. nonrepeatable reads and phantom reads are possible

        [Uncommitted read/Read Uncommited]
        Transactions can access uncomitted changes made by other transactions; transactions are not isolated and dirty reads, nonrepeatable reads and phandtom reads are possbile

## Explain slide 'Comparing isolation levels'

This table summarizes which concurrency problem is resolved by which isolation level. The lost update problem is resolved by all isolation levels

       "Isolation Level"       "Lost update"   "Dirty Read"    "Non-repeatable Read"   "Phantom Read"
        Repeatable Read (RR)    -               -               -                       -
        Read Stability (RS)     -               -               -                       Possible
        Cursor Stability (CS)   -               -               Possible                Possible
        Uncommitted Read (UR)   -               Possible        Possible                Possible

## Compare and contrast lock timeout and deadlock detector

- Lock timeout:
  Specifies the number of seconds that an application will wait to obtain a lock helping avoid glboale deadlocks for applciation

- Deadlock detector:
  The deadlock runs at a set interval and if it finds a deadlock is resolves the deadlock by db2's algorithms

## Find out how locks affect concurrency, performance and data integrity.

    It's like having an triangle where you put a keyword to every single corner.
    You must choose one of the properties and must dispence two of the others
    For example if you want a high level of data integrity you would lock at every single transaction the hole database,
    which would decrease the concurrency and performance.

## How do you decide which isolation level to use

- Uncommitted Read isolation level only if you are executing queries on read-only databases
  or if you are executing queries and do not care if those queries return uncommitted data values.
- Cursor Stability isolation level when you want maximum concurrency without seeing uncommitted data values
- Read Stability isolation level when you want concurrency and you want qualified rows
  to remain stable forthe duration of an individual transaction
- Repeatable Read isolation level if you are executing queries and
  changes to the result data sets produced are unacceptable
