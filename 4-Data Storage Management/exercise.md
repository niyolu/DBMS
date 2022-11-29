CONNECT TO DB2CERT;

CREATE REGULAR TABLESPACE dms01 MANAGED BY DATABASE
   USING (FILE 'c:\dms\dms01.data' 25) EXTENTSIZE 4;

db2 LIST TABLESPACES SHOW DETAIL

           Tablespaces for Current Database

 Tablespace ID                        = 0
 Name                                 = SYSCATSPACE
 Type                                 = Database managed space
 Contents                             = All permanent data. Regular table space.
 State                                = 0x0000
   Detailed explanation:
     Normal
 Total pages                          = 32768
 Useable pages                        = 32764
 Used pages                           = 28952
 Free pages                           = 3812
 High water mark (pages)              = 28952
 Page size (bytes)                    = 4096
 Extent size (pages)                  = 4
 Prefetch size (pages)                = 4
 Number of containers                 = 1

 Tablespace ID                        = 1
 Name                                 = TEMPSPACE1
 Type                                 = System managed space
 Contents                             = System Temporary data
 State                                = 0x0000
   Detailed explanation:
     Normal
 Total pages                          = 1
 Useable pages                        = 1
 Used pages                           = 1
 Free pages                           = Not applicable
 High water mark (pages)              = Not applicable
 Page size (bytes)                    = 4096
 Extent size (pages)                  = 32
 Prefetch size (pages)                = 32
 Number of containers                 = 1

 Tablespace ID                        = 2
 Name                                 = USERSPACE1
 Type                                 = Database managed space
 Contents                             = All permanent data. Large table space.
 State                                = 0x0000
   Detailed explanation:
     Normal
 Total pages                          = 8192
 Useable pages                        = 8160
 Used pages                           = 736
 Free pages                           = 7424
 High water mark (pages)              = 736
 Page size (bytes)                    = 4096
 Extent size (pages)                  = 32
 Prefetch size (pages)                = 32
 Number of containers                 = 1

 Tablespace ID                        = 3
 Name                                 = SYSTOOLSPACE
 Type                                 = Database managed space
 Contents                             = All permanent data. Large table space.
 State                                = 0x0000
   Detailed explanation:
     Normal
 Total pages                          = 8192
 Useable pages                        = 8188
 Used pages                           = 152
 Free pages                           = 8036
 High water mark (pages)              = 152
 Page size (bytes)                    = 4096
 Extent size (pages)                  = 4
 Prefetch size (pages)                = 4
 Number of containers                 = 1

 Tablespace ID                        = 4
 Name                                 = DMS01
 Type                                 = Database managed space
 Contents                             = All permanent data. Regular table space.
 State                                = 0x0000
   Detailed explanation:
     Normal
 Total pages                          = 25
 Useable pages                        = 20
 Used pages                           = 12
 Free pages                           = 8
 High water mark (pages)              = 12
 Page size (bytes)                    = 4096
 Extent size (pages)                  = 4
 Prefetch size (pages)                = 4
 Number of containers                 = 1

 Tablespace ID                        = 5
 Name                                 = DMS02
 Type                                 = Database managed space
 Contents                             = All permanent data. Regular table space.
 State                                = 0x0000
   Detailed explanation:
     Normal
 Total pages                          = 23
 Useable pages                        = 20
 Used pages                           = 6
 Free pages                           = 14
 High water mark (pages)              = 6
 Page size (bytes)                    = 4096
 Extent size (pages)                  = 2
 Prefetch size (pages)                = 2
 Number of containers                 = 1

 Tablespace ID                        = 6
 Name                                 = DMS03
 Type                                 = Database managed space
 Contents                             = All permanent data. Large table space.
 State                                = 0x0000
   Detailed explanation:
     Normal
 Total pages                          = 89
 Useable pages                        = 80
 Used pages                           = 24
 Free pages                           = 56
 High water mark (pages)              = 24
 Page size (bytes)                    = 4096
 Extent size (pages)                  = 8
 Prefetch size (pages)                = 8
 Number of containers                 = 1

 Tablespace ID                        = 7
 Name                                 = DMS04
 Type                                 = Database managed space
 Contents                             = All permanent data. Regular table space.
 State                                = 0x0000
   Detailed explanation:
     Normal
 Total pages                          = 21
 Useable pages                        = 18
 Used pages                           = 6
 Free pages                           = 12
 High water mark (pages)              = 6
 Page size (bytes)                    = 4096
 Extent size (pages)                  = 2
 Prefetch size (pages)                = 2
 Number of containers                 = 1

 Tablespace ID                        = 8
 Name                                 = DMS05
 Type                                 = Database managed space
 Contents                             = All permanent data. Regular table space.
 State                                = 0x0000
   Detailed explanation:
     Normal
 Total pages                          = 17
 Useable pages                        = 14
 Used pages                           = 6
 Free pages                           = 8
 High water mark (pages)              = 6
 Page size (bytes)                    = 4096
 Extent size (pages)                  = 2
 Prefetch size (pages)                = 2
 Number of containers                 = 1

 Tablespace ID                        = 9
 Name                                 = DMS06
 Type                                 = Database managed space
 Contents                             = All permanent data. Regular table space.
 State                                = 0x0000
   Detailed explanation:
     Normal
 Total pages                          = 33
 Useable pages                        = 28
 Used pages                           = 12
 Free pages                           = 16
 High water mark (pages)              = 12
 Page size (bytes)                    = 4096
 Extent size (pages)                  = 4
 Prefetch size (pages)                = 4
 Number of containers                 = 1

 Tablespace ID                        = 10
 Name                                 = SMS01
 Type                                 = System managed space
 Contents                             = All permanent data. Regular table space.
 State                                = 0x0000
   Detailed explanation:
     Normal
 Total pages                          = 2
 Useable pages                        = 2
 Used pages                           = 2
 Free pages                           = Not applicable
 High water mark (pages)              = Not applicable
 Page size (bytes)                    = 4096
 Extent size (pages)                  = 4
 Prefetch size (pages)                = 8
 Number of containers                 = 2




C:\Users\Administrator\Documents>db2 LIST TABLESPACE CONTAINERS FOR 10

            Tablespace Containers for Tablespace 10

 Container ID                         = 0
 Name                                 = c:\sms\sms01
 Type                                 = Path

 Container ID                         = 1
 Name                                 = c:\sms\sms02
 Type                                 = Path



C:\Users\Administrator\Documents>db2 LIST TABLESPACE CONTAINERS FOR 4

            Tablespace Containers for Tablespace 4

 Container ID                         = 0
 Name                                 = c:\dms\dms01.data
 Type                                 = File



C:\Users\Administrator\Documents>db2 ALTER TABLESPACE DMS03 ADD (FILE 'c:\dms\more' 723)
DB20000I  The SQL command completed successfully.



C:\Users\Administrator\Documents>db2 ALTER TABLESPACE DMS05 PREFETCHSIZE 64
DB20000I  The SQL command completed successfully.



db2 -tvf tabscreat.sql
COMMIT
DB20000I  The SQL command completed successfully.

CREATE DISTINCT TYPE INFO       AS CLOB(512K)
DB21034E  The command was processed as an SQL statement because it was not a
valid Command Line Processor command.  During SQL processing it returned:
SQL0601N  The name of the object to be created is identical to the existing
name "ADMINISTRATOR.INFO" of type "DATA TYPE".  SQLSTATE=42710

CREATE DISTINCT TYPE PIC        AS BLOB(1M)
DB21034E  The command was processed as an SQL statement because it was not a
valid Command Line Processor command.  During SQL processing it returned:
SQL0601N  The name of the object to be created is identical to the existing
name "ADMINISTRATOR.PIC" of type "DATA TYPE".  SQLSTATE=42710

CREATE TABLE books   ( bookno   SMALLINT     NOT NULL, title    VARCHAR(50)  NOT NULL, authno   SMALLINT     NOT NULL ) IN dms04 INDEX IN dms05
DB20000I  The SQL command completed successfully.

CREATE TABLE speaker ( authno   SMALLINT     NOT NULL, date     DATE         NOT NULL, city     VARCHAR(25)  NOT NULL) IN dms04
DB20000I  The SQL command completed successfully.

CREATE TABLE stock   ( bookno   SMALLINT     NOT NULL, price    DECIMAL(4,2) NOT NULL WITH DEFAULT, qty      INTEGER) IN dms06 INDEX in dms02
DB20000I  The SQL command completed successfully.

CREATE TABLE reorder ( bookno    SMALLINT    NOT NULL, TIMESTAMP TIMESTAMP) IN sms01
DB20000I  The SQL command completed successfully.

CREATE TABLE author  ( authno    SMALLINT    NOT NULL, name      VARCHAR(50) NOT NULL, speaker   CHAR(1)     NOT NULL WITH DEFAULT, bio       INFO, picture   PIC ) IN dms01 INDEX in dms02 long in dms03
DB20000I  The SQL command completed successfully.

CREATE INDEX bknum ON books(bookno)
DB20000I  The SQL command completed successfully.

CREATE INDEX stnum ON stock(bookno)
DB20000I  The SQL command completed successfully.

CREATE INDEX aunum ON author(authno)
DB20000I  The SQL command completed successfully.

CREATE INDEX aunam ON author(name)
DB20000I  The SQL command completed successfully.

COMMIT
DB20000I  The SQL command completed successfully.


db2 LIST TABLESPACES SHOW DETAIL

           Tablespaces for Current Database

 Tablespace ID                        = 0
 Name                                 = SYSCATSPACE
 Type                                 = Database managed space
 Contents                             = All permanent data. Regular table space.
 State                                = 0x0000
   Detailed explanation:
     Normal
 Total pages                          = 32768
 Useable pages                        = 32764
 Used pages                           = 28960
 Free pages                           = 3804
 High water mark (pages)              = 28960
 Page size (bytes)                    = 4096
 Extent size (pages)                  = 4
 Prefetch size (pages)                = 4
 Number of containers                 = 1

 Tablespace ID                        = 1
 Name                                 = TEMPSPACE1
 Type                                 = System managed space
 Contents                             = System Temporary data
 State                                = 0x0000
   Detailed explanation:
     Normal
 Total pages                          = 1
 Useable pages                        = 1
 Used pages                           = 1
 Free pages                           = Not applicable
 High water mark (pages)              = Not applicable
 Page size (bytes)                    = 4096
 Extent size (pages)                  = 32
 Prefetch size (pages)                = 32
 Number of containers                 = 1

 Tablespace ID                        = 2
 Name                                 = USERSPACE1
 Type                                 = Database managed space
 Contents                             = All permanent data. Large table space.
 State                                = 0x0000
   Detailed explanation:
     Normal
 Total pages                          = 8192
 Useable pages                        = 8160
 Used pages                           = 736
 Free pages                           = 7424
 High water mark (pages)              = 736
 Page size (bytes)                    = 4096
 Extent size (pages)                  = 32
 Prefetch size (pages)                = 32
 Number of containers                 = 1

 Tablespace ID                        = 3
 Name                                 = SYSTOOLSPACE
 Type                                 = Database managed space
 Contents                             = All permanent data. Large table space.
 State                                = 0x0000
   Detailed explanation:
     Normal
 Total pages                          = 8192
 Useable pages                        = 8188
 Used pages                           = 152
 Free pages                           = 8036
 High water mark (pages)              = 152
 Page size (bytes)                    = 4096
 Extent size (pages)                  = 4
 Prefetch size (pages)                = 4
 Number of containers                 = 1

 Tablespace ID                        = 4
 Name                                 = DMS01
 Type                                 = Database managed space
 Contents                             = All permanent data. Regular table space.
 State                                = 0x0000
   Detailed explanation:
     Normal
 Total pages                          = 25
 Useable pages                        = 20
 Used pages                           = 20
 Free pages                           = 0
 High water mark (pages)              = 20
 Page size (bytes)                    = 4096
 Extent size (pages)                  = 4
 Prefetch size (pages)                = 4
 Number of containers                 = 1

 Tablespace ID                        = 5
 Name                                 = DMS02
 Type                                 = Database managed space
 Contents                             = All permanent data. Regular table space.
 State                                = 0x0000
   Detailed explanation:
     Normal
 Total pages                          = 23
 Useable pages                        = 20
 Used pages                           = 18
 Free pages                           = 2
 High water mark (pages)              = 18
 Page size (bytes)                    = 4096
 Extent size (pages)                  = 2
 Prefetch size (pages)                = 2
 Number of containers                 = 1

 Tablespace ID                        = 6
 Name                                 = DMS03
 Type                                 = Database managed space
 Contents                             = All permanent data. Large table space.
 State                                = 0x0000
   Detailed explanation:
     Normal
 Total pages                          = 812
 Useable pages                        = 792
 Used pages                           = 56
 Free pages                           = 736
 High water mark (pages)              = 56
 Page size (bytes)                    = 4096
 Extent size (pages)                  = 8
 Prefetch size (pages)                = 16
 Number of containers                 = 2

 Tablespace ID                        = 7
 Name                                 = DMS04
 Type                                 = Database managed space
 Contents                             = All permanent data. Regular table space.
 State                                = 0x0000
   Detailed explanation:
     Normal
 Total pages                          = 21
 Useable pages                        = 18
 Used pages                           = 14
 Free pages                           = 4
 High water mark (pages)              = 14
 Page size (bytes)                    = 4096
 Extent size (pages)                  = 2
 Prefetch size (pages)                = 2
 Number of containers                 = 1

 Tablespace ID                        = 8
 Name                                 = DMS05
 Type                                 = Database managed space
 Contents                             = All permanent data. Regular table space.
 State                                = 0x0000
   Detailed explanation:
     Normal
 Total pages                          = 17
 Useable pages                        = 14
 Used pages                           = 12
 Free pages                           = 2
 High water mark (pages)              = 12
 Page size (bytes)                    = 4096
 Extent size (pages)                  = 2
 Prefetch size (pages)                = 64
 Number of containers                 = 1

 Tablespace ID                        = 9
 Name                                 = DMS06
 Type                                 = Database managed space
 Contents                             = All permanent data. Regular table space.
 State                                = 0x0000
   Detailed explanation:
     Normal
 Total pages                          = 33
 Useable pages                        = 28
 Used pages                           = 20
 Free pages                           = 8
 High water mark (pages)              = 20
 Page size (bytes)                    = 4096
 Extent size (pages)                  = 4
 Prefetch size (pages)                = 4
 Number of containers                 = 1

 Tablespace ID                        = 10
 Name                                 = SMS01
 Type                                 = System managed space
 Contents                             = All permanent data. Regular table space.
 State                                = 0x0000
   Detailed explanation:
     Normal
 Total pages                          = 3
 Useable pages                        = 3
 Used pages                           = 3
 Free pages                           = Not applicable
 High water mark (pages)              = Not applicable
 Page size (bytes)                    = 4096
 Extent size (pages)                  = 4
 Prefetch size (pages)                = 8
 Number of containers                 = 2