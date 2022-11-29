# Lab 4 chat questions - Data Storage Management
Before doing the lab

## 1. Describe the storage objects: tablespace, buffer pool, container.

- Tablespace
- Buffer Pool
- Container

## 2. Explain the overhead of a data page.
Regardless of the page size used, the first 76 bytes of a page are reserved for the
DB2 Database Manager’s use and the remaining bytes are available for user data.
Keep in mind that because LOB data is not stored directly in a row, LOB columns
only take up 24 bytes of a page— the amount of space required to store a reference
to the LOB data value’s location.)

## 3. Explain the purpose of large object descriptors.
For better disk and cache performance large objects are stored outside the regular rows with references in the form of object descriptors (file system descriptors?)

## 4. Explain an index. Talk about advantages and disadvantages.
Indexes are ordered key-pointer pairs stored in an efficient datastructure (B+ Trees/LSM-Trees) for improved row query performance

## 5. Explain a container.
Its a thingy usually associated with a physical device but also directory/file names. It makes up table spaces

## 6. Explain an extent.
Block of storage within a table space container defining the number of pages and extra memory to be allocated when an extent reaches its space limit. (?)

Database manager loadbalances across containers, the write size before switching is called an extent

## 7. Explain prefetch.
DB2 uses heuristic algorithms for pre-loading resources into buffer pools.

## 8. Read the document for the lab exercise. Add your own questions, at least one.
## 9. Do the calculation and share your results with your classmates.