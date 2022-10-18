# Getting Sarted

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
- `DB2INSTANCE=DB2`
- `DB2PATH=C:\Program Files\IBM\SQLLIB`
  
##### 3. What is the command to list out all the defined DB2 profile registry variables for the DB2 server?sd
`db2set -all`


##### 4. Is DB2COMM a valid DB2 profile registry variable? What command can be used to validate it?
`db2set -lr`

---

# Questions


