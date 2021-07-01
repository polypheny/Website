---
layout: plain
title: Data Partitioning
---

Data partitioning generally enables a system to process data concurrently and to some extent even in parallel. Considering that access to data can be 
efficiently load balanced and therefore enhances the throughput per query.
Data partitioning is a widely used concept among DBMS, to split data in chunks or fragments of relevance
and therefore achieve efficient access and parallel processing.

In general data partitioning in Polypheny can be distinguished between two variations:

* [Vertical Partitioning](#vertical-partitioning)
* [Horizontal Partitioning](#horizontal-partitioning)

## Vertical Partitioning

## Horizontal Partitioning
Refers to the partitioning of objects like tables into a disjoint set of rows that can be stored and accessed separetely.
To support this explicit form of partitioning there exist several partition [algorithms](#existing-horizontal-partition-algorithms).
These algorithms can be applied to a table based on an arbitary column which results in a fragmentation of the table 
based on the data values of the selected column.

### Existing Horizontal Partition Algorithms

Currently Polypheny supports the following partition functions:
* **List** - the table is partitioned by explicitly assigning values to each partition. These placements are the result of the extended vertical partitoning of a table.
* **Hash** - the table is partitioned by specifying a modulus and a remainder for each partition. Each partition will hold the rows for which the hash value of the partition key divided by the specified modulus will produce the specified remainder
* **Range** - the table is partitioned into numerical "ranges" defined by a key column, with no overlap between  the ranges of values assigned to different partitions. 

## Vertical + Horizontal Partitioning

### Current Limitations

### Roadmap

* **Temperature Aware Partitioning** - a partition function which places data based on its "temperature" which classifies data entities depending on certain parameters like the access frequency


