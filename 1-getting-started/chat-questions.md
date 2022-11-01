- [1. Command Line Processor / Command Line Shell](#1-command-line-processor--command-line-shell)
- [2. Command Line vs. Graphical User Interface](#2-command-line-vs-graphical-user-interface)
- [3. Compare environment variables with profile registry variables.](#3-compare-environment-variables-with-profile-registry-variables)
- [4. Five ways to end a connection to a database. Tell the difference. Think about loss of data.](#4-five-ways-to-end-a-connection-to-a-database-tell-the-difference-think-about-loss-of-data)
- [5. Instance vs database](#5-instance-vs-database)
- [6. Which database objects are you familiar with? Describe the database objects.](#6-which-database-objects-are-you-familiar-with-describe-the-database-objects)
- [7. Database Object "schema"](#7-database-object-schema)
- [8. Read the document for the lab exercise. Add your own questions, at least one.](#8-read-the-document-for-the-lab-exercise-add-your-own-questions-at-least-one)

#### 1. Command Line Processor / Command Line Shell

1. **What is a Command Line Processor (CLP)?**
   
   db2 CLI with several modes, including an interactive setting. It enables CLP commands and SQL statements.
2. **Which other Command Line Processors than the one of DB2 do you know?**
   
   The use of the term CLP is limited to IBM. However CLI's are pretty common, including interactive REPL's for programming languages and configuration/control related interfaces for tools/services such as docker CLI, npm, routers, ssh clients (application level tools in general).
3. **What is the difference between Command Line Processor and Command Line Window?**
   
   The Command Line Window is used to initialize a CPL environment.
4. **When would you use the DB2 Command Line Processor in interactive mode, no interactive mode, and batch mode?**
   
   - **`interactive mode`** - protoyping, exploration/experimentation
   - **`command mode`** - ad-hoc changes
   - **`batch mode`** - automation
5. **Give some examples of Command Line Processor (CLP) commands.**
   
   - The `ACTIVATE DATABASE` command activates the specified database and starts up all necessary database services so that the database is available for connection and use by any application.
   - The `ATTACH` command enables an application to specify the instance at which instance-level commands (`CREATE DATABASE` and `FORCE APPLICATION`, for example) are to be executed. This instance can be the current instance, another instance on the same workstation, or an instance on a remote workstation.
   - The `CREATE DATABASE` command initializes a new database with an optional user-defined collating sequence, creates the three initial table spaces, creates the system tables, and allocates the recovery log file. When you initialize a new database, the `AUTOCONFIGURE` command is issued by default.
   - The `DROP DATABASE` command deletes the database contents and log files for the database, uncatalogs the database, and deletes the database subdirectory.
   - The `ECHO` command permits the user to write character strings to standard output.
   - The `PING` command tests the network response time of the underlying connectivity between a client and a connected database server. 
   
6. **Explain the difference between CLP commands and DMBS system commands. Name some DBMS system commands.**
   
   DBMS controls the entire installation while CLP is instance based.
   - `db2mtrk` - Provides complete report of memory status, for instances, databases, agents, and applications.
   - `db2sampl` - Create sample database command.

#### 2. Command Line vs. Graphical User Interface
1. **When would you prefer using a graphical user interface and when would you prefer using a command line?**
   
   I try to generally avoid using GUIs if there exists a CLI. Monitoring or displaying graphics would be the exception.

2. **What are the advantages and disadvantages of both interfaces?**
   
   CLIs have higher learning curves than (good) GUIs but bring more flexibility to the table, like automation scripts which open up a plethora of possibilities. Once accustomed to a CLI, there will be less changes through software updates and lots of parallels to other CLI so usage tends to be less of a hustle and less error prone over time. GUIs have the advantage of embedded media as opposed to colored ASCII graphics.

#### 3. Compare environment variables with profile registry variables.

1. **What are those variables used for?**
   
Windows environment variables are used by the CLP and probably some more db2 tools to config their context in the OS.
Profile registry variables configure aspects about the DBMS itself.
1. **What is similar? Are there any differences? How to set them?**
   
- OS: can be non-persistent on system or shell-session level, are issued by using `set`.
- db2: controlled by `db2set` command.
1. **Where are registry variables located on Windows?**
   
`%SystemRoot%\System32\config`
1. **How to get a list of all supported registry variables?**
   
`db2set -lr`
1. **How to get the current instance?**
   
`set | findstr DB2INSTANCE` or `echo %DB2INSTANCE%`

#### 4. Five ways to end a connection to a database. Tell the difference. Think about loss of data.
- **`connect reset`** - reboot the connection, graceful
- **`disconnect`** - destroy the connection, graceful
- **`terminate`** - terminate the application, same as disonnect
- **`force application`** - terminates the application immediately, losing the connection ungracefully and risking loss of data
- **`stop force`** - I have no idea what im talking about

#### 5. Instance vs database
1. **Explain the difference between a database and an instance.**
   
An instance is a logical database manager environment where you catalog databases. Thus Several databases can live in an instance while several instances can run on a single server. Having multiple instances is motivated by dev/prod parity, environment specific tuning/optimization, confidentiality, redundance (availability).
1. **Locate a database and an instance on your computer. Where would you look for them?**
   
See environment variable `DB2PATH`.
#### 6. Which database objects are you familiar with? Describe the database objects.
A database object is any defined object in a database that is used to store or reference data. Some examples of database objects include:
- tables
- views
- aliases
- schemas
- indexes
- user-defined data types.
#### 7. Database Object "schema"
1. **For the SQL-Statement “select * from labor.headers” identify the database you are connected to, the schema you are working in and the table you are retrieving data.**
   
the database is called labor, idk what the other stuff is
1. **Explain what a schema is and give examples how you could benefit from its use.**
   
Structure of a database described in a formal language. Formally it is the set of formulas called integrity constraints that are to be imposed on database.
#### 8. Read the document for the lab exercise. Add your own questions, at least one.
How do you disable autocommits?