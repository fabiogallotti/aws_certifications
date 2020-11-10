# DynamoDB #

## Introduction ##

It's a Key-Value and Document NOSQL database, which can guarantee consistent reads and writes at any scale.

* **NOSQL** = database that is not relational and doesn't use SQL to query data
* **Key-Value** store = form of data storage with keys that reference a value
* **Document** store = form of data storage which has nested data structures

A table in DynamoDB is made by **Items** (rows) and **Attributes** (columns). A **Key** is the name of an attribute. A **Value** is the actual data.

**Main features:**

* multi-region
* multi-master
* durable
* built-in security
* backup/restore
* in-memory caching
* all data are stored in an SSD storage and spread across **three different Availability Zones**
* provides **Eventual** and **Strong** consistent reads; when data need to be updated, the change has to be done on all the three replicas. It's possible to have data inconsistency if reading from a copy not yet updated:
  * **Eventual** (default)
    * it's possible to have inconsistent copies
    * reads are fast
    * no guarantee of consistency
    * it **becomes consistent** in around 1 second, eventually
  * **Strong**
    * when updating, no response is given before everything is consistent
    * higher latency, slower reads
    * guarantee of consistency in max 1 second

## Main Concepts ##

* **Partition**, it's an allocation of storage for a table, backed by a Solid State Drive (SSD) and automatically replicated across multiple AZs in a region. It speeds up reads for large tables (slice your table in smaller chunks of data). DynamoDB automatically creates partitions as the data grow:
  * every 10 Gb of data
  * when exceeded 3000 RCU (Read Capacity Units) or 1000 WCU (Write Capacity Units) for a partition

* **Primary Key**, it has to be defined at table creation and cannot be changed later. Determines where and how data will be stored in partitions. Generally you want keys *unique* and *uniform* (evenly divide data). There are 2 types:
  * **Simple**, using only a partition key
  * **Composite**, using both partition (HASH) and sorting (RANGE) key; the records in the same partition will be kept together sorted alphabetically

* **Query**, allow to find items in a table based on primary keys value
  * can query any table that has a composite primary key
  * reads are eventually consistent
  * returns all attributes for items
  * you can return specific attributes using *ProjectExpression*
  * sorted ascending (use *ScanIndexForward* = False for descending)

* **Scans**, allow to scan all items in a table and return one or more items through filters
  * returns all attributes for items
  * you can return specific attributes using *ProjectExpression*
  * operation are sequentials
  * less efficient than queries
  * as the table grows, scans takes longer
  * for a large table a scan can use all provisioned capacity

* **Provisioned Capacity**, two types:
  * **Throughput**, it's the maximum amount of capacity that your app is allowd to read/write per second from a table
    * measured in RCU and WCU
    * can automatically scale up or down based on utilization
    * if you exceed the capacity you are throttling, so requests are dropped (data loss)
  * **On-Demand**, pay per request.
    * no provisioned capacity
    * no auto scaling
    * upper limits: 40.000 RCU, 40.000 WCU
    * good for unpredictable traffic

* **Read Capacity Unit**, represents for an item up to 4 Kb in size:
  * 1 strongly consistent read per second
  * 2 eventually consistent reads per second
  * Calculation:
    * **Strong Consistency**:
      1) Round up the size to the nearest multiple of 4
      2) divide by 4
      3) multiply by the number of reads

      50 reads, 40 Kb per item = 500 RCUs
    * **Eventual Consistency**
      1) Round up the size to the nearest multiple of 4
      2) divide by 4
      3) multiply by the number of reads
      4) divide by 2 and round to the next integer

      50 reads, 40 Kb per item = 250 RCUs

* **Write Capacity Unit**, represent for an item up to 1 Kb, 1 write per second
  * Calculation:
    1) Round up the size to the next integer
    2) multiply by the number of writes

    50 writes, 40 Kb per item = 2000 RCUs

* **Streams**, when enabled on a table, DynamoDB captures every modification to items, so you can react. If insert, update, delete occurs, the change will be captured and sent to a Lambda function (no RCU consumed).
  * changes are sent in batches to the Lambda
  * changes are sent to Lambda in near real-time
  * each stream record appeard exactly in the stream
  * for each item that is modified, the stream records appear in the same sequence of the actual modifications

* **Global Tables**, solution for deploying a multi-region, multi-master DB, without having to maintain the replicas. You must have:
  * KMS CMK
  * enable Streams
  * Stream type of New and Old Image

* **Transaction**, it's a change that occurs in the DB. If any dependent condition fails, the transaction will be rolled-back. They are ACID (Atomicity, Consistency, Isolation, Durability).
  * DynamoDB performs transaction at no additional cost using *TransactWriteItems* and *TransactGetItems*
  * DynamoDB allows for *all-or-nothing* changes to multiple items both within and across multile tables
  * DynamoDB performs two underlying reads and writes of every item in the transaction, one to prepare and one to commit (consume RCU, WCU)
  * *ConditionCheck* used to do preconditional checks

* **Time to Live (TTL)**, let's you have items that expire at a given time. It's useful for keeping a DB small for temporary continuous data (like monitoring, logs).
  * You need to provide an attribute name in DateTime format: DynamoDB doesn't supports date, so it's a string in Epoch format.

* **Errors**:
  * *ThrottlingException*, if the rate of requests exceeds the allowed throughput capacity. Can happen with *CreateTable*, *UpdateTable*, *DeleteTable*
  * *ProvisionedThroughputExceededException*, if the maximum allowed provisione throughput capacity is exceeded. The AWS SDK will automatically retry with **Exponential Backoff** (again after 50ms, 100ms, 200ms, up to 1 minute)

* **Secondary Index**, is a copy of selected columns of data which is used to quickly sort. Two types in DynamoDB:
  * **Local** (LSI)
    * only with the initial table
    * can provide strong consistency
    * every partition is scoped to a partition that has the same partition key value
    * total size can't be more than 10 Gb
    * shares the same provisioned throughput capacity for read and write as the table it's indexing
    * max 5 per table
    * cannot be added, modified, deleted after creation of the table
    * needs both **partition** (must be the same as the base table) and **sort** keys (should be different)
    * you can request attributes that are not projected into the index
  * **Global** (GSI)
    * cannot provide strong consistency
    * queries on the index can span all the data in the base table, across all partitions
    * no size restriction
    * it has it's own provisioned throughput capacity
    * max 20 per table
    * can be added, modified, deleted at any time
    * needs only **partition** key (should be different)
    * you cannot request attributes that are not projected into the index

* **DynamoDB Accelerator (DAX)**
  * it's a in-memory cache for DynamoDB that runs in a cluster
  * DynamoDB response times are usually milliseconds, DAX can reduce to microseconds
  * it's eventual consistent
  * a DAX cluster consists of one or more nodes
  * each node runs its own instance of the DAX caching software
  * one of the nodes serves as the primary node for the cluster, additional nodes are read replicas
  * an app can access DAX by specifing the endpoint for the DAX cluster
  * performs intelligent load balancing and routing
  * incoming requests are evenly distributed across all nodes in the cluster
  * **Ideal** for apps that:
    * require the fastest possible response time
    * read a small number of item frequently
    * are read-intensive and requires repeated reads
  * **Not ideal** for apps that:
    * need strong consistent reads
    * don't require microseconds response times
    * are write-intensive
    * in these case you can use ElastiCache

## Useful Commands ##

* `aws dynamodb get-item`, returns set of attributes for the item with the given primary key
* `aws dynamodb put-item`, creates or replaces an item
* `aws dynamodb update-item`, edits the attributes of an item
* `aws dynamodb batch-get-item`, returns attributes of one or more items
* `aws dynamodb batch-write-item`, puts or deletes multiple items in one or more tables
* `aws dynamodb create-table`, add a new table
* `aws dynamodb update-table`, modifies settings for a table
* `aws dynamodb delete-table`, deletes a table
* `aws dynamodb transact-get-items`, synchronous operation that retrieves multiple items from one or more tables
* `aws dynamodb transact-write-items`, synchronous write operation
* `aws dynamodb query`, finds items based on primary key values
