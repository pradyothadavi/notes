# HBase

HBase is a Java-based, open source, NoSQL, non-relational, column-oriented, distributed database built on top of the Hadoop Distributed Filesystem (HDFS), modeled after Google’s BigTable paper.

HBase was designed with availability over consistency and offers high availability of all its services with a fast and automatic failover.

The ability to allow creation and usage of a flexible data model.

In a column-oriented database, the system stores data tables as sparse columns of data rather than as entire rows of data.

## HBase Principles

### Table Format

In HBase, you will find two different types of tables: the system tables and the user tables.Systems tables are used internally by HBase to keep track of meta information like the table’s access control lists (ACLs), metadata for the tables and regions, namespaces, and so on.There should be no need for you to look at those tables.User tables are what you will create for your use cases.They will belong to the default namespace unless you create and use a specific one.

#### Table Layout

The HBase world uses many different words to describe different parts: rows, columns, keys, cells, values, KeyValues, timestamps, and more.To make sure we talk about the same thing, here is a clarification: a row is formed of multiple columns, all referenced by the same key.A specific column and a key are called a cell.It is possible to have multiple versions of the same cell, all differentiated by the timestamp.A cell can also be called a KeyValue pair.So a row, referenced by a key, is formed of a group of cells, each being a specific column for the given row.

column families need to be defined at the table creation, there is no need to define the column names in advance.

To allow a faster lookup access, keys and columns are alphabetically sorted within a table but also in memory.

HBase orders the keys based on the byte values, so “AA” will come before “BB”. If you store numbers as character chains, keep in mind that “1234” will come before “9”. If you have to store numbers, then to save on space and to keep the ordering, you will need to store their byte representation. In this model, the integer 1234 will be stored as 0x00 0x00 0x04 0xD2, while 9 will be 0x00 0x00 0x00 0x09. Sorting those two values, we can see that 0x00 0x00 0x00 0x09 will come before 0x00 0x00 0x04 0xD2.

Because they will be used to create files and directories in the filesystem, the table name and the column family names need to use only printable characters.

#### Table Storage

On a RegionServer, you will have as many memstores as you have regions multiplied by the number of column families receiving writes, all sharing the same reserved memory area.

- **RegionServer**

Each region will have a start key and an end key that will define its boundaries.All this information will be stored within the files into the region but also into the hbase:meta table.

- **Column Family**

A column family is an HBase-specific concept that you will not find in other RDBMS applications.

The write cache memory area for a given RegionServer is shared by all the column families configured for all the regions hosted by the given host. Abusing column families will put pressure on the memstore, which will generate many small files, which in turn will generate a lot of compactions that might impact the performance. There is no technical limitation on the number of column families you can configure for a table. However, over the last three years, most of the use cases we had the chance to work on only required a single column family. Some required two column families, but each time we have seen more than two column families, it has been possible and recommended to reduce the number to improve efficiency. If your design includes more than three column families, you might want to take a deeper look at it and see if all those families are really required; most likely, they can be regrouped. If you do not have any consistency constraints between your two columns families and data will arrive into them at a different time, instead of creating two column families for a single table, you can also create two tables, each with a single column family. This strategy is useful when it comes time to decide the size of the regions. Indeed, while it was better to keep the two column families almost the same size, by splitting them accross two different tables, it is now easier to let me grow independently.

- **Stores**

A store object regroups one memstore and zero or more store files (called HFiles). This is the entity that will store all the information written into the table and will also be used when data needs to be read from the table.

- **HFiles**

HFiles are created when the memstores are full and must be flushed to disk. HFiles are eventually compacted together over time into bigger files. They are the HBase file format used to store table data. HFiles are composed of different types of blocks (e.g., index blocks and data blocks). HFiles are stored in HDFS, so they benefit from Hadoop persistence and replication.

- **Blocks**

HFile blocks are usually between 8 KB and 1 MB, but the default size is 64 KB.

Different blocks are

- Data block
- Index block
- Bloom filter block
- Trailer block

- **Cells**

The “key type” field represents the different possible HBase operations

The maximum length for the row key plus the column family and the column qualifier is stored as four bytes and is 2^31 – 1 – 12 or, 2,147,483,635 (key length).

The maximum length for the value is stored as four bytes and is 2^31 – 1 or 2,147,483,647 (value length).

The maximum length for the row key is stored as two signed bytes and is 32,767 (row length).

Because it is stored in one signed byte, the maximum length for the column family is 127 (CF length).

The maximum length for all the tags together is stored as two bytes and is 65,535 (tags length).
