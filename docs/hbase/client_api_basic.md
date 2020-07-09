# Client API : Basic

## General Notes

The primary client interface to HBase is the HTable class.

All operations that mutate data are guaranteed to be    atomic on a per-row basis. This affects all other    concurrent readers and writers of that same row. In other words, it does    not matter if another client or thread is reading from or writing to the    same row: they either read a consistent last mutation, or may have to wait    before being able to apply their change.

Each    instantiation involves scanning the .META. table to check if the table actually    exists and if it is enabled, as well as a few other operations that make    this call quite costly. Therefore, it is recommended that you create    HTable instances only once—and one per    thread—and reuse that instance for the rest of the lifetime of your client    application.

## CRUD Operations

### PUT Method

