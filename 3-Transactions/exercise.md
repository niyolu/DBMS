# Transactions


- [Transactions](#transactions)
    - [Objectives](#objectives)
- [Exercises](#exercises)
  - [Part A - Lock Timeout](#part-a---lock-timeout)
    - [1. If DB2CERT does not already exist, create the database, tables and populate data with the createDB2CERT.ddl file: `db2 –tvf createDB2CERT.ddl`](#1-if-db2cert-does-not-already-exist-create-the-database-tables-and-populate-data-with-the-createdb2certddl-file-db2-tvf-createdb2certddl)
    - [2. Make sure the DB2 instance is started successfully. Open two DB2 Command Windows (window A and B). To examine the DB2 locking behavior, we want to control the commit scope. Turn `AUTOCOMMIT` off for the two windows just opened by setting the environment variable `DB2OPTIONS`. Check the value of `AUTOMMIT` for both windows!!! Using the Control Center to set `DB2OPTIONS` instead will make changes permanent, but keep this in mind for the upcoming labs. Connect to `DB2CERT` in both windows.](#2-make-sure-the-db2-instance-is-started-successfully-open-two-db2-command-windows-window-a-and-b-to-examine-the-db2-locking-behavior-we-want-to-control-the-commit-scope-turn-autocommit-off-for-the-two-windows-just-opened-by-setting-the-environment-variable-db2options-check-the-value-of-autommit-for-both-windows-using-the-control-center-to-set-db2options-instead-will-make-changes-permanent-but-keep-this-in-mind-for-the-upcoming-labs-connect-to-db2cert-in-both-windows)
    - [3. What is the deadlock check time and lock wait time for the DB2CERT database? Check the database configuration.](#3-what-is-the-deadlock-check-time-and-lock-wait-time-for-the-db2cert-database-check-the-database-configuration)
    - [4. Change the database configuration LOCKTIMEOUT to 20 seconds. Note that this parameter is in units of seconds not in milliseconds as for `DLCHKTIME`.](#4-change-the-database-configuration-locktimeout-to-20-seconds-note-that-this-parameter-is-in-units-of-seconds-not-in-milliseconds-as-for-dlchktime)
  - [Part B - Isolation Levels and Cursors](#part-b---isolation-levels-and-cursors)
    - [1. We are now going to look at how DB2 locking mechanism behaves for each isolation level.](#1-we-are-now-going-to-look-at-how-db2-locking-mechanism-behaves-for-each-isolation-level)
    - [2. Repeat step 1 using all of the DB2 isolation levels. Write down which lock will obtain the table and which locks will obtain the rows](#2-repeat-step-1-using-all-of-the-db2-isolation-levels-write-down-which-lock-will-obtain-the-table-and-which-locks-will-obtain-the-rows)
      - [RR (Repeatable Read)](#rr-repeatable-read)
      - [CS (Cursor Stability)](#cs-cursor-stability)
      - [RS (Read Stability)](#rs-read-stability)
      - [UR (Uncommited read)](#ur-uncommited-read)
      - [Locks](#locks)
- [Questions](#questions)


### Objectives
In these exercises, we will:
- Demonstrate lock timeout
- Investigate different isolation levels

# Exercises

## Part A - Lock Timeout

### 1. If DB2CERT does not already exist, create the database, tables and populate data with the createDB2CERT.ddl file: `db2 –tvf createDB2CERT.ddl`

### 2. Make sure the DB2 instance is started successfully. Open two DB2 Command Windows (window A and B). To examine the DB2 locking behavior, we want to control the commit scope. Turn `AUTOCOMMIT` off for the two windows just opened by setting the environment variable `DB2OPTIONS`. Check the value of `AUTOMMIT` for both windows!!! Using the Control Center to set `DB2OPTIONS` instead will make changes permanent, but keep this in mind for the upcoming labs. Connect to `DB2CERT` in both windows.

```bash
>> set DB2OPTIONS=+c
>> set | findstr DB2
DB2CLP=DB20FADE
DB2INSTANCE=DB2
DB2OPTIONS=+c
```

In window A, enter:
```bash
(@DB2, ADMINIST@DB2CERT)select * from test

NUMBER NAME                                               TYPE CUT_SCORE LENGTH TOTALTAKEN TOTALPASSED
------ -------------------------------------------------- ---- --------- ------ ---------- -----------
500    DB2 Fundamentals                                   P        65.00     90          0           0
501    DB2 Administration                                 P        60.00    180          0           0
502    DB2 Application Development                        P        55.00    180          0           0

3 record(s) selected.

(@DB2, ADMINIST@DB2CERT)update test set cut_score = 80 where char(number) = '500'
DB20000I  The SQL command completed successfully.
```
In window B, enter:
```bash
select * from test

NUMBER NAME                                               TYPE CUT_SCORE LENGTH TOTALTAKEN TOTALPASSED
------ -------------------------------------------------- ---- --------- ------ ---------- -----------
500    DB2 Fundamentals                                   P        65.00     90          0           0
501    DB2 Administration                                 P        60.00    180          0           0
502    DB2 Application Development                        P        55.00    180          0           0

  3 record(s) selected.
```

- **What happened? Do both SQL statements execute successfully with the expected return code or result?**
Both transactions are successful but the changes from A are not present in B.


- **Why?**
  The first transaction wasn't commited


- **What happens if a commit is issued in window A?**
  A:
  ```bash
  (@DB2, ADMINIST@DB2CERT)commit
  DB20000I  The SQL command completed successfully.
  ```
  B:
  ```bash
  (@DB2, ADMINIST@DB2CERT)select * from test

  NUMBER NAME                                               TYPE CUT_SCORELENGTH TOTALTAKEN TOTALPASSED
  ------ -------------------------------------------------- ---- --------------- ---------- -----------
  500    DB2 Fundamentals                                   P        8000     90          0           0
  501    DB2 Administration                                 P        6000    180          0           0
  502    DB2 Application Development                        P        5500    180          0           0

  3 record(s) selected.
  ```

### 3. What is the deadlock check time and lock wait time for the DB2CERT database? Check the database configuration.
```bash
>> db2 get db configuration | findstr "Lock lock"
Max storage for lock list (4KB)              (LOCKLIST) = AUTOMATIC(13984)
Percent. of lock lists per application       (MAXLOCKS) = AUTOMATIC(98)
Interval for checking deadlock (ms)         (DLCHKTIME) = 10000
Lock timeout (sec)                        (LOCKTIMEOUT) = -1
Block log on disk full                (BLK_LOG_DSK_FUL) = NO
Block non logged operations            (BLOCKNONLOGGED) = NO
Lock timeout events                   (MON_LOCKTIMEOUT) = NONE
Deadlock events                          (MON_DEADLOCK) = WITHOUT_HIST
Lock wait events                         (MON_LOCKWAIT) = NONE
Lock wait event threshold               (MON_LW_THRESH) = 5000000
Lock event notification level         (MON_LCK_MSG_LVL) = 1
```
`LOCKTIMEOUT` = -1, `DLCHKTIME` = 10000ms


### 4. Change the database configuration LOCKTIMEOUT to 20 seconds. Note that this parameter is in units of seconds not in milliseconds as for `DLCHKTIME`.


**Disconnect all connections to the DB2CERT database so that the above change can take into effect. Ensure that all connections (applications) are stopped. If not, force them to stop. Then restart those you need**

- **In window A, enter:**
  ```bash
  >> db2 update test set cut_score = 70
  DB20000I  The SQL command completed successfully.
  ```
- **In window B, enter:**
  ```bash
  >> db2 update test set cut_score = 80
  DB21034E  The command was processed as an SQL statement because it was not a
  valid Command Line Processor command.  During SQL processing it returned:
  SQL0911N  The current transaction has been rolled back because of a deadlock
  or timeout.  Reason code "68".  SQLSTATE=40001
  ```

**Window B waits for window A to release its locks. The condition is a normal locking scenario and not a deadlock condition. Window B will wait for 20 seconds and then DB2 will initiate a rollback of the transaction in window B. The code `SQLCODE –911N` with reason `code 68` is returned.**


## Part B - Isolation Levels and Cursors

### 1. We are now going to look at how DB2 locking mechanism behaves for each isolation level.
**Window A**:
- **In window A Disconnect from the database**
  ```bash
  >> db2 connect reset
  DB20000I  The SQL command completed successfully.
  ```
- **Change isolation level to Repeatable Read**
  ```bash
  >> db2 change isolation to rr
  DB21053W  Automatic escalation will occur when you connect to a database that
  does not support RR.
  DB20000I  The CHANGE ISOLATION command completed successfully.
  ```
- **Connect to the database DB2CERT**
  `db2 connect to db2cert`
- **Define a cursor with the command:**
  ```bash
  db2 declare cur1 cursor for
      SELECT cid,number,score
      FROM test_taken
      WHERE char(cid) ='333333333'
  ```
  or execute `cursor.ddl`:
  ```bash
  >> db2 -tvf cursor.ddl
  DECLARE cur1 CURSOR FOR SELECT cid, number, scorE FROM test_taken WHERE CHAR(cid) ='333333333'
  DB20000I  The SQL command completed successfully.
  ```
  The cursor is called `cur1` and it is defined as a SELECT statement based on all of the tests taken by candidate with `id` = '333333333'
- Open the `cur1` cursor, enter:
  ```bash
  >> db2 open cur1
  DB20000I  The SQL command completed successfully.
  ```
- Fetch the first row of data, enter:
  ```bash
  >> db2 fetch cur1

  CID       NUMBER SCORE
  --------- ------ --------
  333333333 500           -

  1 record(s) selected.
  ```
- Repeat the FETCH command until the end of the result table.
  > same as before until 0 selected recoreds

**Window B**:
- **In window B, use the snapshot monitor to examine locks obtained:**
  ```bash
  >> db2 connect to db2cert
  Database Connection Information
  Database server        = DB2/NT64 11.1.1.1
  SQL authorization ID   = ADMINIST...
  Local database alias   = DB2CERT

  >> db2 update monitor switches using lock on
  DB20000I  The UPDATE MONITOR SWITCHES command completed successfully.
  
  >> db2 get snapshot for locks on db2cert
  ```
- Discuss the list of locks returned by each snapshot

### 2. Repeat step 1 using all of the DB2 isolation levels. Write down which lock will obtain the table and which locks will obtain the rows

#### RR (Repeatable Read)
```bash
>> db2 get snapshot for locks on db2cert

Database Lock Snapshot

Database name                              = DB2CERT
Database path                              = C:\DB2\NODE0000\SQL00002\MEMBER0000\
Input database alias                       = DB2CERT
Locks held                                 = 3
Applications currently connected           = 2
Agents currently waiting on locks          = 0
Snapshot timestamp                         = 11/22/2022 21:52:45.544870

Lock Name                   = 0x02000700000000000000000054
Lock Attributes             = 0x00000000
Release Flags               = 0x00000001
Lock Count                  = 1
Hold Count                  = 0
Lock Object Name            = 7
Object Type                 = Table
Tablespace Name             = USERSPACE1
Table Schema                = ADMINISTRATOR
Table Name                  = TEST_TAKEN
Mode                        = S
```

#### CS (Cursor Stability)

```bash
>> db2 get snapshot for locks on db2cert

            Database Lock Snapshot

Database name                              = DB2CERT
Database path                              = C:\DB2\NODE0000\SQL00002\MEMBER0000\
Input database alias                       = DB2CERT
Locks held                                 = 3
Applications currently connected           = 2
Agents currently waiting on locks          = 0
Snapshot timestamp                         = 11/22/2022 22:11:40.364692

...

List Of Locks
 Lock Name                   = 0x02000700000000000000000054
 Lock Attributes             = 0x00000000
 Release Flags               = 0x40000000
 Lock Count                  = 1
 Hold Count                  = 0
 Lock Object Name            = 7
 Object Type                 = Table
 Tablespace Name             = USERSPACE1
 Table Schema                = ADMINISTRATOR
 Table Name                  = TEST_TAKEN
 Mode                        = IS
```

#### RS (Read Stability)
```bash
>> db2 get snapshot for locks on db2cert
Database Lock Snapshot

Database name                              = DB2CERT
Database path                              = C:\DB2\NODE0000\SQL00002\MEMBER0000\
Input database alias                       = DB2CERT
Locks held                                 = 6
Applications currently connected           = 2
Agents currently waiting on locks          = 0
Snapshot timestamp                         = 11/22/2022 22:19:55.364934

List Of Locks
Lock Name                   = 0x02000700000000000000000054
Lock Attributes             = 0x00000000
Release Flags               = 0x00000001
Lock Count                  = 1
Hold Count                  = 0
Lock Object Name            = 7
Object Type                 = Table
Tablespace Name             = USERSPACE1
Table Schema                = ADMINISTRATOR
Table Name                  = TEST_TAKEN
Mode                        = IS
```

#### UR (Uncommited read)
```bash
>> db2 get snapshot for locks on db2cert

Database Lock Snapshot

Database name                              = DB2CERT
Database path                              = C:\DB2\NODE0000\SQL00002\MEMBER0000\
Input database alias                       = DB2CERT
Locks held                                 = 3
Applications currently connected           = 2
Agents currently waiting on locks          = 0
Snapshot timestamp                         = 11/22/2022 22:22:11.403429

List Of Locks
Lock Name                   = 0x02000700000000000000000054
Lock Attributes             = 0x00000000
Release Flags               = 0x40000000
Lock Count                  = 1
Hold Count                  = 0
Lock Object Name            = 7
Object Type                 = Table
Tablespace Name             = USERSPACE1
Table Schema                = ADMINISTRATOR
Table Name                  = TEST_TAKEN
Mode                        = IN
```



#### Locks

For Repeatable Read isolation level, a Share (S) lock was obtained for the
TEST_TAKEN table. For Read Stability isolation level, three Share (NS) lock
were obtained for rows of the TEST_TAKEN table. For Uncommitted Read isolation level, an Intent None (IN) lock was
obtained for the TEST_TAKEN table. 

- **Share (S)**
  Read-only lock for owner and all concurrent applications. An unlocked table is lockable on row-level.

- **Intent Share (IS)**
  The lock owner has read-only capabilities on the locked table but doesn't acquire row-level locks allowing concurrent applications to read and change data. When an IS lock is owned by a transaction it acquires a share lock on each read row. The intent lock is acquired when a transaction does not convey the intent to update any rows in the table

- **Intent None (IN)**
  Lock owner can read data in the locked table including uncommitted data. No changes. No row-level locks possible, so other concurrent applications can read and change data in the table.

# Questions
- Is behaviour of Part A exercise 2. correct? Shouldn't transaction B have waited for A to commit via locks?
- Validity of Part B
- What is a `none-lock` good for?

