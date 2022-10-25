****# Getting Sarted

[comment]: <> (Delete next Line as it was generated as a bulletpoint by VSCODE Extension)


- [Getting Sarted](#getting-sarted)
    - [Objectives](#objectives)
    - [Part A](#part-a)
        - [2. Examine the operating system environment variable settings. What is the DB2 instance currently set to? What is the installation path of DB2?](#2-examine-the-operating-system-environment-variable-settings-what-is-the-db2-instance-currently-set-to-what-is-the-installation-path-of-db2)
        - [3. What is the command to list out all the defined DB2 profile registry variables for the DB2 server?sd](#3-what-is-the-command-to-list-out-all-the-defined-db2-profile-registry-variables-for-the-db2-serversd)
        - [4. Is DB2COMM a valid DB2 profile registry variable? What command can be used to validate it?](#4-is-db2comm-a-valid-db2-profile-registry-variable-what-command-can-be-used-to-validate-it)
- [Questions](#questions)

### Objectives
In these exercises, we will:
− Use the DB2 Command Window to perform most of the steps listed
below
− Examine the environment that DB2 runs in
− Examine the DB2 profile registry
− Create the SAMPLE database
− Use DB2 manuals for reference

---

### Part A

##### 2. Examine the operating system environment variable settings. What is the DB2 instance currently set to? What is the installation path of DB2?
via `set | findstr DB2*`:
- `DB2INSTANCE=DB2`
- `DB2PATH=C:\Program Files\IBM\SQLLIB`

alternatively one could do:
```bash
  >> echo %DB2INSTANCE%
```
##### 3. What is the command to list out all the defined DB2 profile registry variables for the DB2 server?sd
`db2set -all`


##### 4. Is DB2COMM a valid DB2 profile registry variable? What command can be used to validate it?
- display all valid variables via `db2set -lr`:
  ```bash
  >> set -lr | findstr DB2COMM
  DB2COMM
  ```
- `db2set <VARIABLE>` prints information about a valid variable and an error on invalid ones:
  ```bash
    >> db2set DB2COMM

    DBI1303W  Variable not set.

    Explanation:

    The variable was not set in the profile registry.

    User response:

    No further action is required.
  ```


##### 5. `DB2COMM` specifies the communication managers to be started when the instance (also known as database manager) is started. This allows remote connection to the databases defined in the instance via protocol set with this DB2 profile registry variable. Set the DB2 profile registry variable `DB2COMM=TCPIP` on instance level. If this is not set, no DB2 communications managers are started at the server. (Changes in DB2 profile registry variables will take in effect after the instance is stopped and restarted. We will recycle the instance later.)
```bash
>> db2set DB2COMM=TCPIP
```
##### 6. Besides the DB2 instance, what other instances are defined in the DB2 server?
```bash
>> db2ilist
DEVELOP
DB2
```
additional instances can be created via `db2icrt <name>`.

##### 7. Obtain a list of databases within the DB2 instance.
```bash
>> db2 list db directory
SQL1057W  The system database directory is empty.  SQLSTATE=01606
```

---

# Questions


