# Getting Connected

- [Getting Connected](#getting-connected)
    - [Objectives](#objectives)
- [Exercises](#exercises)
    - [1. Open a DB2 Command Window. How many instances are available? What is the current instance? How many databases are cataloged in the DB2 instance? Obtain the following information for the SAMPLE database: Database name, Database alias name, Directory entry type, Database drive or Node name](#1-open-a-db2-command-window-how-many-instances-are-available-what-is-the-current-instance-how-many-databases-are-cataloged-in-the-db2-instance-obtain-the-following-information-for-the-sample-database-database-name-database-alias-name-directory-entry-type-database-drive-or-node-name)
    - [2. Connect to the database SAMPLE and select from the EMPLOYEE table. Insert another employee into the EMPLOYEE table with your firstname and lastname.](#2-connect-to-the-database-sample-and-select-from-the-employee-table-insert-another-employee-into-the-employee-table-with-your-firstname-and-lastname)
    - [3. Customize your CLP prompt by using the DB2_CLPPROMPT registry variable. This will show you instance attachment, database connection and user authorization. So, you will not get lost in the following exercises.](#3-customize-your-clp-prompt-by-using-the-db2_clpprompt-registry-variable-this-will-show-you-instance-attachment-database-connection-and-user-authorization-so-you-will-not-get-lost-in-the-following-exercises)
    - [4. You are now enabling one of your instances for being accessed by a remote client:](#4-you-are-now-enabling-one-of-your-instances-for-being-accessed-by-a-remote-client)
    - [5. Let your classmate catalog your instance and your database by telling him your current IP-address, which comes from the title of your RDP-window, e.g. 18.156.82.154 for a title like “ec2-18-156-82-154.eu-central- 1.compute.amazonaws.com”. See next step how to catalog. Follow the manipulation of your data done by your classmate.](#5-let-your-classmate-catalog-your-instance-and-your-database-by-telling-him-your-current-ip-address-which-comes-from-the-title-of-your-rdp-window-eg-1815682154-for-a-title-like-ec2-18-156-82-154eu-central--1computeamazonawscom-see-next-step-how-to-catalog-follow-the-manipulation-of-your-data-done-by-your-classmate)
    - [6. Make your computer a client to access a remote server run by one of your classmates:](#6-make-your-computer-a-client-to-access-a-remote-server-run-by-one-of-your-classmates)
    - [7. Examine the node and database directories, for each instance separately.](#7-examine-the-node-and-database-directories-for-each-instance-separately)
    - [8. Connect to the remote RMTSAMP database as user Administrator. Select all rows from the EMPLOYEE table. Show the proof that you really see the remote EMPLOYEE table of your classmate instead of yours. Insert another employee into the EMPLOYEE table with your firstname and lastname.](#8-connect-to-the-remote-rmtsamp-database-as-user-administrator-select-all-rows-from-the-employee-table-show-the-proof-that-you-really-see-the-remote-employee-table-of-your-classmate-instead-of-yours-insert-another-employee-into-the-employee-table-with-your-firstname-and-lastname)
    - [9. Open a second DB2 Command Window. Let user Su connect to the local SAMPLE database using Lab2-Usr as password. Get a list of all tables.](#9-open-a-second-db2-command-window-let-user-su-connect-to-the-local-sample-database-using-lab2-usr-as-password-get-a-list-of-all-tables)
    - [10. Open a third DB2 Command Window. Let user Bob connect to the remote RMTSAMP database using Lab2-Usr as password. Get a list of all tables.](#10-open-a-third-db2-command-window-let-user-bob-connect-to-the-remote-rmtsamp-database-using-lab2-usr-as-password-get-a-list-of-all-tables)
    - [11. Switch back to your first DB2 Command Window. List out all connections to the current instance DB2. Which applications do you expect to be connected, which ones are missing, why are they missing?](#11-switch-back-to-your-first-db2-command-window-list-out-all-connections-to-the-current-instance-db2-which-applications-do-you-expect-to-be-connected-which-ones-are-missing-why-are-they-missing)
    - [12. Attach to node RMTNODE. List out all the connections to RMTNODE.](#12-attach-to-node-rmtnode-list-out-all-the-connections-to-rmtnode)
    - [13. Force the application of Bob to stop.](#13-force-the-application-of-bob-to-stop)
    - [14. Switch to Bob’s DB2 Command Windows. Try to get a list of all tables. What](#14-switch-to-bobs-db2-command-windows-try-to-get-a-list-of-all-tables-what)
    - [15. Detach from node RMNODE.](#15-detach-from-node-rmnode)

### Objectives
Examine the DB2 node and database directories
- Catalog nodes and databases using the DB2 Command Window
- Connect to a remote database
- Attach to a remote node

---

# Exercises

### 1. Open a DB2 Command Window. How many instances are available? What is the current instance? How many databases are cataloged in the DB2 instance? Obtain the following information for the SAMPLE database: Database name, Database alias name, Directory entry type, Database drive or Node name

```bash
>> db2ilist
DEVELOP
DB2

>> set | findstr DB2*
DB2INSTANCE=DB2
DB2PATH=C:\Program

>> db2 list db directory

System Database Directory
Number of entries in thedirectory = 1
Database 1 entry:
Databasealias                       =SAMPLE
Databasename                        =SAMPLE
Local databasedirectory             = C:
Database releaselevel               = 14.00
Comment                             =
Directory entrytype                 = Indirect
Catalog database partitionnumber    = 0
Alternate serverhostname            =
Alternate server portnumber         =
```

### 2. Connect to the database SAMPLE and select from the EMPLOYEE table. Insert another employee into the EMPLOYEE table with your firstname and lastname.
```bash
>> db2 connect to SAMPLE

Database Connection Information

 Database server        = DB2/NT64 11.1.1.1
 SQL authorization ID   = ADMINIST...
 Local database alias   = SAMPLE


>> db2
...
```
```SQL
db2 => SELECT * FROM EMPLOYEE

EMPNO  FIRSTNME     MIDINIT LASTNAME        WORKDEPT PHONENO HIREDATE   JOB      EDLEVEL SEX BIRTHDATE  SALARY      BONUS       COMM
------ ------------ ------- --------------- -------- ------- ---------- -------- ------- --- ---------- ----------- ----------- -----------
000010 CHRISTINE    I       HAAS            A00      3978    01/01/1995 PRES          18 F   08/24/1963   152750.00     1000.00     4220.00
000020 MICHAEL      L       THOMPSON        B01      3476    10/10/2003 MANAGER       18 M   02/02/1978    94250.00      800.00     3300.00


db2 => INSERT INTO employee (empno, firstnme, lastname, edlevel) VALUES (42069, 'Nils', 'Lubenius', 99)
DB20000I  The SQL command completed successfully.
```

### 3. Customize your CLP prompt by using the DB2_CLPPROMPT registry variable. This will show you instance attachment, database connection and user authorization. So, you will not get lost in the following exercises.

```bash
>> db2set DB2_CLPPROMPT=(%ia@%i," "%da@%d)

>> db2
(@DB2, @)connect to sample

Database Connection Information

Database server        = DB2/NT64 11.1.1.1
SQL authorization ID   = ADMINIST...
Local database alias   = SAMPLE

(@DB2, ADMINIST@SAMPLE)
```

### 4. You are now enabling one of your instances for being accessed by a remote client:

- Set your current instance to DEVELOP
  `set DB2INSTANCE=DEVELOP`
- Set TCP as communication protocol
  `db2set DB2COMM=tcpip` 
- Set service db2c_develop to listen on port 50004 
  - update dbm cfg using SVCENAME db2c_develop;
    ```bash
    >> db2 update dbm cfg using SVCENAME db2c_develop
    DB20000I  The UPDATE DATABASE MANAGER CONFIGURATION command completed successfully.
    ```
  - open C:\Windows\system32\drivers\etc\services and add db2c_DEVELOP 50004/TCP (already done by lecturer)
    `db2c_DEVELOP	 50004/tcp                           #DB2 instance DEVELOP`
- Start instance DEVELOP
  ```bash
  >> db2start
  SQL1063N  DB2START processing was successful.
  ```
- Create sample database
  ```bash
  >> db2sampl

  Creating database "SAMPLE"...
  Connecting to database "SAMPLE"...
  Creating tables and data in schema "ADMINISTRATOR"...
  Creating tables with XML columns and XML data in schema "ADMINISTRATOR"...

  'db2sampl' processing complete.
  ```
- Configure your windows firewall to allow inbound communication via TCP port 50004 (already done by lecturer)
  ![Firewall Settings](./src/firewall.png)

- NOTES:
  The port has to be set via `db2 update dbm cfg using SVCENAME 50004` (not sure why the db2c_develop cmd was needed).
  To enforce the catalog changes restart the manager: 
  1. `db2 terminate`
  2. `db2stop`
  3. `db2start`

  To verify the tcp connection:
  ```bash
  >> netstat -tan | findstr 50004
  TCP    0.0.0.0:50004          0.0.0.0:0              LISTENING       InHost
  TCP    [::]:50004             [::]:0                 LISTENING       InHost
  ```

### 5. Let your classmate catalog your instance and your database by telling him your current IP-address, which comes from the title of your RDP-window, e.g. 18.156.82.154 for a title like “ec2-18-156-82-154.eu-central- 1.compute.amazonaws.com”. See next step how to catalog. Follow the manipulation of your data done by your classmate.

### 6. Make your computer a client to access a remote server run by one of your classmates:

- Set your current instance to DB2
  `set DB2INSTANCE=DB2`
- Catalog a TCPIP node. Use TCPIP as protocol, ask one of your classmates
for his IP-address as hostname, use 50004 as services name (which is
actually the port number of the instance), use DEVELOP as instance
name, and omit other optional clauses. Name this node entry RMTNODE.
  ```bash
  (@DB2, @)catalog tcpip node RMTNODE remote <REMOTE_IP> server 50004 remote_instance DEVELOP
  DB20000I  The CATALOG TCPIP NODE command completed successfully.
  DB21056W  Directory changes may not be effective until the directory cache is
  refreshed
  ```

- Catalog the remote database SAMPLE. USE RMTSAMP as database
alias, RMTNODE as node name, SERVER as authentication type, and
omit other optional clauses. Why using a database alias?
  ```bash
  (@DB2, @)catalog database SAMPLE as RMTSAMP at node RMTNODE authentication SERVER
  DB20000I  The CATALOG DATABASE command completed successfully.
  DB21056W  Directory changes may not be effective until the directory cache is
  refreshed.
  ```
  The alias is used to differentiate between the local and remote databases named DEVELOP.

### 7. Examine the node and database directories, for each instance separately.

- DB2:
  ```bash
  >> db2 list db directory

  System Database Directory
  Number of entries in the directory = 2

  Database 1 entry:

  Database alias                       = RMTSAMP
  Database name                        = SAMPLE
  Node name                            = RMTNODE
  Database release level               = 14.00
  Comment                              =
  Directory entry type                 = Remote
  Authentication                       = SERVER
  Catalog database partition number    = -1
  Alternate server hostname            =
  Alternate server port number         =

  Database 2 entry:

  Database alias                       = SAMPLE
  Database name                        = SAMPLE
  Local database directory             = C:
  Database release level               = 14.00
  Comment                              =
  Directory entry type                 = Indirect
  Catalog database partition number    = 0
  Alternate server hostname            =
  Alternate server port number         =

  >> db2 list node directory

  Node Directory

  Number of entries in the directory = 1

  Node 1 entry:

  Node name                      = RMTNODE
  Comment                        =
  Directory entry type           = LOCAL
  Protocol                       = TCPIP
  Hostname                       = <REMOTE_IP>
  Service name                   = 50004
  ```

- DEVELOP:
  ```bash
  >> db2 list db directory

  System Database Directory

  Number of entries in the directory = 1

  Database 1 entry:

  Database alias                       = SAMPLE
  Database name                        = SAMPLE
  Local database directory             = C:
  Database release level               = 14.00
  Comment                              =
  Directory entry type                 = Indirect
  Catalog database partition number    = 0
  Alternate server hostname            =
  Alternate server port number         =

  >> db2 list node director
  SQL1027N  The node directory cannot be found.
  ```

### 8. Connect to the remote RMTSAMP database as user Administrator. Select all rows from the EMPLOYEE table. Show the proof that you really see the remote EMPLOYEE table of your classmate instead of yours. Insert another employee into the EMPLOYEE table with your firstname and lastname.
```bash
>> db2 connect to RMTSAMP user ADMINISTRATOR
Enter current password for ADMINISTRATOR:

Database Connection Information

Database server        = DB2/NT64 11.1.1.1
SQL authorization ID   = ADMINIST...
Local database alias   = RMTSAMP


(@DB2, ADMINIST@RMTSAMP)INSERT INTO employee (empno, firstnme, lastname, edlevel) VALUES (42069, 'Nils', 'Lubenius', 99)
DB20000I  The SQL command completed successfully.

(@DB2, ADMINIST@RMTSAMP)SELECT * FROM EMPLOYEE WHERE FIRSTNME='Michael'

EMPNO  FIRSTNME     MIDINIT LASTNAME        WORKDEPT PHONENO HIREDATE   JOB      EDLEVEL SEX BIRTHDATE  SALARY      BONUS       COMM
------ ------------ ------- --------------- -------- ------- ---------- -------- ------- --- ---------- ----------- ----------- -----------
000000 Michael      -       Mustermann        -        -       -          -             99 -   -                    -           -           -

1 record(s) selected.
```

### 9. Open a second DB2 Command Window. Let user Su connect to the local SAMPLE database using Lab2-Usr as password. Get a list of all tables.

```bash
(@DB2, @)connect to SAMPLE user Su


(@DB2, SU      @SAMPLE)list tables

Table/View                      Schema          Type  Creation time
------------------------------- --------------- ----- --------------------------

  0 record(s) selected.

(@DB2, SU      @SAMPLE) list tables for schema ADMINISTRATOR

Table/View                      Schema          Type  Creation time
------------------------------- --------------- ----- --------------------------
ACT                             ADMINISTRATOR   T     2022-10-25-23.51.22.181003
...
ADEFUSR                         ADMINISTRATOR   S     2022-10-25-23.51.23.
614002

  47 record(s) selected.
```

### 10. Open a third DB2 Command Window. Let user Bob connect to the remote RMTSAMP database using Lab2-Usr as password. Get a list of all tables.

```bash
(@DB2, @)connect to SAMPLE user Bob

(@DB2, SU      @SAMPLE)list tables

Table/View                      Schema          Type  Creation time
------------------------------- --------------- ----- --------------------------

0 record(s) selected.

(@DB2, SU      @SAMPLE) list tables for schema ADMINISTRATOR

Table/View                      Schema          Type  Creation time
------------------------------- --------------- ----- --------------------------
ACT                             ADMINISTRATOR   T     2022-10-25-23.51.22.181003
...
ADEFUSR                         ADMINISTRATOR   S     2022-10-25-23.51.23.
614002

47 record(s) selected.
```

### 11. Switch back to your first DB2 Command Window. List out all connections to the current instance DB2. Which applications do you expect to be connected, which ones are missing, why are they missing?

```bash
(@DB2, ADMINIST@RMTSAMP)list applications show detail

CONNECT Auth Id                                                                                                                  Application Name     Appl.      Application Id                                                 Seq#  Number of  Coordinating     Coordinator     Status                         Status Change Time         Node     DB Name  DB Path
                                                                                                                                                      Handle                                                                          Agents     member number    pid/thread
-------------------------------------------------------------------------------------------------------------------------------- -------------------- ---------- -------------------------------------------------------------- ----- ---------- ---------------- --------------- ------------------------------ -------------------------- -------- -------- --------------------
SU                                                                                                                               db2lused             13         *LOCAL.DB2.221111172527                                        00001 1          0                2480            Connect Completed              Not Collected              EC2AMAZ- SAMPLE   C:\DB2\NODE0000\SQL00001\MEMBER0000\
ADMINISTRATOR                                                                                                                    db2evml_DB2DETAILDEA 19         *LOCAL.DB2.221111172533                                        00001 1          0                2700            Connect Completed              Not Collected              EC2AMAZ- SAMPLE   C:\DB2\NODE0000\SQL00001\MEMBER0000\
SU                                                                                                                               db2wlmd              12         *LOCAL.DB2.221111172526                                        00001 1          0                1680            Connect Completed              Not Collected              EC2AMAZ- SAMPLE   C:\DB2\NODE0000\SQL00001\MEMBER0000\
SU                                                                                                                               db2taskd             11         *LOCAL.DB2.221111172525                                        00001 1          0                812             Connect Completed              Not Collected              EC2AMAZ- SAMPLE   C:\DB2\NODE0000\SQL00001\MEMBER0000\
SU                                                                                                                               db2pcsd              17         *LOCAL.DB2.221111172531                                        00001 1          0                2924            Connect Completed              Not Collected              EC2AMAZ- SAMPLE   C:\DB2\NODE0000\SQL00001\MEMBER0000\
SU                                                                                                                               db2stmm              10         *LOCAL.DB2.221111172524                                        00001 1          0                680             Connect Completed              Not Collected              EC2AMAZ- SAMPLE   C:\DB2\NODE0000\SQL00001\MEMBER0000\
SU                                                                                                                               db2fw1               16         *LOCAL.DB2.221111172530                                        00001 1          0                2476            Connect Completed              Not Collected              EC2AMAZ- SAMPLE   C:\DB2\NODE0000\SQL00001\MEMBER0000\
SU                                                                                                                               db2bp.exe            9          *LOCAL.DB2.221111172523                                        00005 1          0                3264            UOW Waiting                    Not Collected              EC2AMAZ- SAMPLE   C:\DB2\NODE0000\SQL00001\MEMBER0000\
SU                                                                                                                               db2fw0               15         *LOCAL.DB2.221111172529                                        00001 1          0                2492            Connect Completed              Not Collected              EC2AMAZ- SAMPLE   C:\DB2\NODE0000\SQL00001\MEMBER0000\
SU                                                                                                                               db2dbctrld           14         *LOCAL.DB2.221111172528                                        00001 1          0                2516            Connect Completed              Not Collected              EC2AMAZ- SAMPLE   C:\DB2\NODE0000\SQL00001\MEMBER0000\

```

### 12. Attach to node RMTNODE. List out all the connections to RMTNODE.

```bash
(@DB2, ADMINIST@RMTSAMP)attach to RMTNODE user Administrator using Database22ws

Instance Attachment Information

Instance server        = DB2/NT64 11.1.1.1
Authorization ID       = ADMINIST...
Local instance alias   = RMTNODE


(ADMINIST@RMTNODE, ADMINIST@RMTSAMP)list applications show detail

CONNECT Auth Id                                                                                                                  Application Name     Appl.      Application Id                                                 Seq#  Number of  Coordinating     Coordinator     Status                         Status Change Time         Node     DB Name  DB Path
                                                                                                                                                      Handle                                                                          Agents     member number    pid/thread
-------------------------------------------------------------------------------------------------------------------------------- -------------------- ---------- -------------------------------------------------------------- ----- ---------- ---------------- --------------- ------------------------------ -------------------------- -------- -------- --------------------
ADMINISTRATOR                                                                                                                    db2dbctrld           32         *LOCAL.DB2.221111171934                                        00001 1          0                1596            Connect Completed              Not Collected              EC2AMAZ- SAMPLE   C:\DB2\NODE0000\SQL00001\MEMBER0000\
BOB                                                                                                                              db2bp.exe            58         <REMOTE_IP>.49751.221111173237                                00004 1          0                6060            UOW Waiting                    Not Collected              EC2AMAZ- SAMPLE   C:\DB2\NODE0000\SQL00001\MEMBER0000\
ADMINISTRATOR                                                                                                                    db2lused             31         *LOCAL.DB2.221111171933                                        00001 1          0                1340            Connect Completed              Not Collected              EC2AMAZ- SAMPLE   C:\DB2\NODE0000\SQL00001\MEMBER0000\
ADMINISTRATOR                                                                                                                    db2evml_DB2DETAILDEA 37         *LOCAL.DB2.221111171939                                        00001 1          0                5956            Connect Completed              Not Collected              EC2AMAZ- SAMPLE   C:\DB2\NODE0000\SQL00001\MEMBER0000\
ADMINISTRATOR                                                                                                                    db2wlmd              30         *LOCAL.DB2.221111171932                                        00001 1          0                1536            Connect Completed              Not Collected              EC2AMAZ- SAMPLE   C:\DB2\NODE0000\SQL00001\MEMBER0000\
ADMINISTRATOR                                                                                                                    db2taskd             29         *LOCAL.DB2.221111171931                                        00001 1          0                1188            Connect Completed              Not Collected              EC2AMAZ- SAMPLE   C:\DB2\NODE0000\SQL00001\MEMBER0000\
ADMINISTRATOR                                                                                                                    db2pcsd              35         *LOCAL.DB2.221111171937                                        00001 1          0                2456            Connect Completed              Not Collected              EC2AMAZ- SAMPLE   C:\DB2\NODE0000\SQL00001\MEMBER0000\
ADMINISTRATOR                                                                                                                    db2stmm              28         *LOCAL.DB2.221111171930                                        00001 1          0                824             Connect Completed              Not Collected              EC2AMAZ- SAMPLE   C:\DB2\NODE0000\SQL00001\MEMBER0000\
ADMINISTRATOR                                                                                                                    db2fw1               34         *LOCAL.DB2.221111171936                                        00001 1          0                796             Connect Completed              Not Collected              EC2AMAZ- SAMPLE   C:\DB2\NODE0000\SQL00001\MEMBER0000\
ADMINISTRATOR                                                                                                                    db2bp.exe            27         <REMOTE_IP>.49738.221111171929                                00006 1          0                5836            UOW Waiting                    Not Collected              EC2AMAZ- SAMPLE   C:\DB2\NODE0000\SQL00001\MEMBER0000\
ADMINISTRATOR                                                                                                                    db2fw0               33         *LOCAL.DB2.221111171935                                        00001 1          0                3104            Connect Completed              Not Collected              EC2AMAZ- SAMPLE   C:\DB2\NODE0000\SQL00001\MEMBER0000\
```

### 13. Force the application of Bob to stop.

Look up bobs handle in the connection listing.

```bash
(ADMINIST@RMTNODE, ADMINIST@RMTSAMP) force application (58)
DB20000I  The FORCE APPLICATION command completed successfully.
DB21024I  This command is asynchronous and may not be effective immediately.
```

### 14. Switch to Bob’s DB2 Command Windows. Try to get a list of all tables. What
is the error message?

```bash
list tables
SQL30081N  A communication error has been detected. Communication protocol
being used: "TCP/IP".  Communication API being used: "SOCKETS".  Location
where the error was detected: "18.159.35.228".  Communication function
detecting the error: "recv".  Protocol specific error code(s): "*", "*", "0".
SQLSTATE=08001
```

### 15. Detach from node RMNODE.

```bash
(ADMINIST@RMTNODE, ADMINIST@RMTSAMP)detach
DB20000I  The DETACH command completed successfully.
```