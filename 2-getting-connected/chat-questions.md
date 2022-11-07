#### Prelab
1. **When do we use two instances?**
A common use of environment isolation in software is dev/prod or R&D/prod parity.


1. **Try to compare a node catalog with a telephone directory.**
Telephone numbers are prefixed by coded area information which are similar to IP addresses.

3. **Why do we need database aliases?**
Backwards compatibility

4. **Name some system objects.**
Views, aliases, descriptions, statistics

5. **Do not mix up database catalog and system catalog - tell the difference. (See textbook ch 1, p 63f / ch 2, p 98f / ch 3, p 136)**
Database catalogs contain all locally known database., while the system catalog stores system objects such as

The database holds not only the organization’s operational data, but also a description of this data. For this reason, a database is also defined as a self-describing collection of integrated records. The description of the data is known as the system catalog (or data dictionary or metadata—the “data about data”). It is the self-describing nature of a database that provides program–data independence. (example objects are  views, tables and aliases, schemas, users, applications - metadata.)

names, types, and sizes of data items;
- names of relationships;
- integrity constraints on the data;
- names of authorized users who have access to the data;

- the data items that each user can access and the types of access allowed; for exam-
ple, insert, update, delete, or read access;

- external, conceptual, and internal


6. **What is the difference between connecting to a database and attaching to an instance?**
several databases and their connections per instance

7. **Read the document for the lab exercise. Add your own questions, at least one.**
why do we exist

#### Aftermath
8. **Describe the architecture of the system you built up. Draw a figure. Talk about servers, clients, instances, network.**
9. **Compare and contrast an attachment to an instance done by setting DB2INSTANCE to issuing the attach command.**