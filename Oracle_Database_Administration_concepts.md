**<u>Oracle Data Dictonary</u>**



# Data dictionary

Oracle database **data dictionary**, is a **read-only** set of tables that provides information about the database. 

Purpose of data dictionary:  A data dictionary contains:

- The definitions of all schema objects in the database (tables, views, indexes, clusters, synonyms, sequences, procedures, functions, packages, triggers, and so on)
- How much space has been allocated for, and is currently used by, the schema objects
- Default values for columns
- Integrity constraint information
- The names of Oracle users
- Privileges and roles each user has been granted
- Auditing information, such as who has accessed or updated various schema objects
- Other general database information
- Is owned by SYS user



The data dictionary is a central part of data management for every Oracle database.  Oracle uses data dictionary, in order to perform action such as : 

- Accesses the data dictionary to find information about users, schema objects, and storage structures
- Modifies the data dictionary every time that a DDL statement is issued

Note: Oracle Database stores data dictionary data in tables, just like other data, we can query the data with SQL.





![Description of Figure 8-3 follows](https://docs.oracle.com/en/database/oracle/oracle-database/21/cncpt/img/cncpt_vm_366.png)

