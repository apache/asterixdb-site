---
title: About Apache AsterixDB
---

Apache AsterixDB&trade; is a highly scalable data management system that can store, index, and manage semi-structured
data, e.g., much like MongoDB, but it also supports a full-power query language with the expressiveness of SQL (and
more).
Unlike analytics engines like Apache Hive or Apache Spark, it stores and manages data, so AsterixDB can exploit its
knowledge of data partitioning and the availability of indexes to avoid always scanning data set(s) to process queries.
Somewhat surprisingly, there is no open source parallel database system (relational or otherwise) available to
developers today -- AsterixDB aims to fill this need.

### Core features

* A NoSQL style data model (ADM) based on extending JSON with object
  database concepts.
* An expressive and declarative query language (AQL) for querying
  semi-structured data.
* A runtime query execution engine, Apache Hyracks, for partitioned-parallel
  execution of query plans.
* Partitioned LSM-based data storage and indexing for efficient
  ingestion of newly arriving data.
* Support for querying and indexing external data (e.g., in HDFS) as
  well as data stored within AsterixDB.
* A rich set of primitive data types, including support for spatial,
  temporal, and textual data.
* Indexing options that include B+ trees, R trees, and inverted
  keyword index support.
* Basic transactional (concurrency and recovery) capabilities akin to
  those of a NoSQL store.

### History

Prior to being developed at the Apache Software Foundation AsterixDB was co-developed by a team of faculty, staff, and
students at UC Irvine and UC Riverside. The project was initiated as a large NSF-sponsored project in 2009, the goal of
which was to combine the best ideas from the parallel database world, the then new Apache Hadoop world, and the
semi-structured (e.g., XML/JSON) data world in order to create a next-generation BDMS. A first informal open source
release was made four years later, in June of 2013, under the Apache Software License 2.0. AsterixDB was accepted into
the Apache Incubator in Febuary of 2015 and was established as a TLP in April of 2016.

### More information

More information about AsterixDB (and its underlying frameworks Hyracks and Algebricks) can be found on the site of the
[ASTERIX project at UC Irvine](http://asterix.ics.uci.edu/) - especially in the
[Publications section](http://asterix.ics.uci.edu/publications.html).
