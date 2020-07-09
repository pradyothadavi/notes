# Introduction

[Codd's 12 Rules](https://en.wikipedia.org/wiki/Codd%27s_12_rules#:~:text=Codd%27s%20twelve%20rules%20are%20a,database%20management%20system%20(RDBMS).)

The reason to store values on a per-column basis instead is based on the assumption that, for specific queries, not all of the values are needed.

HBase is    not a column-oriented database in the typical RDBMS    sense, but utilizes an on-disk column storage format. This is also where    the majority of similarities end, because although HBase stores data on    disk in a column-oriented format, it is distinctly different from    traditional columnar databases: whereas columnar databases excel at    providing real-time analytical access to data, HBase excels at providing    key-based access to a specific cell of data, or a sequential    range of cells.

## Nonrelational Database Systems, Not-Only SQL or NoSQL?

### Dimensions

- Data model
- Storage model
- Consistency model
- Physical model
- Read/write performance
- Secondary indexes
- Failure handling
- Compression
- Load balancing
- Atmoic read-modify-write
- Locking, waits, and deadlocks

### DATABASE (DE-)NORMALIZATION

At scale, it is often a requirement that we design schema differently, and a good term to describe this principle is Denormalization, Duplication, and Intelligent Keys (DDI).

## Building Blocks

The most basic unit is a      column. One or more columns form a      row that is addressed uniquely by a row key. A number of rows, in turn,      form a table, and there can be many of them. Each      column may have multiple versions, with each distinct value contained in      a separate cell.

All      columns in a column family are stored together in the same low-level      storage file, called an HFile.

Every column value, or cell, either is      timestamped implicitly by the system or can be set explicitly by the      user.

Different versions of a cell are stored in decreasing timestamp order,      allowing you to read the newest value first.

SortedMap<RowKey, List<SortedMap<Column, List<Value, Timestamp>>>>

Access to row data is atomic and includes      any number of columns being read or written to. There is no further      guarantee or transactional feature that spans multiple rows or across      tables.

### Auto Sharding

Each region is served by exactly one      region server, and each of these servers can      serve many regions at any time.

### Storage API

The API offers operations to create and delete tables and column families. In addition, it has functions to change the table and column family metadata, such as compression or block sizes. Furthermore, there are the usual operations for clients to create or delete values as well as retrieving them with a given row key.

There is also the option to run client-supplied code in the address space of the server. The server-side framework to support this is called coprocessors. The code has access to the server local data and can be used to implement lightweight batch jobs, or use expressions to analyze or summarize data based on a variety of operators.

### Implementation

