# Relational Database Service (RDS) #

## Introduction ##

It's a managed relational database.

* Supports six SQL engines (Aurora, MySQL, MariaDB, Postgres, Oracle, MS SQL Server)
* easy to scale, backup and secure
* you can turn on encryption (with KMS) at-rest for all engines, it will also encrypt backups, snapshots, replicas
* you cannot SSH into the VM running the DB

## Core Concepts ##

* **Backups**
  * Two types:
    * **Automated**
      * choose a Retention Period between 1 and 35 days
      * store transaction logs throughout the day
      * enabled by default
      * stored in S3
    * **Manual Snapshot**
      * taken manually by the user
      * persist even if the original RDS instance is deleted
  * never restored on top of the existing instance; when you restore, a new instance is created for the restored DB, with a new DNS endpoint
* **Multi-AZ**, ensure DB is available if an AZ is unavailable.
  * makes an exact copy of the DB in another AZ
  * automatically sync changes in the main DB to the standy DB
  * there is an automatic Failover protection, if the main AZ is unavailable, the copy is promoted to master
* **Read Replicas**
  * allow to run multiple copies of the DB, with only read access
  * used to improve performance
  * you must have automatic backups enabled
  * asynchronous replication happens between main DB and replicas
  * max 5 replicas
  * each replica has its own DNS endpoint
  * can be Multi-AZ or even Cross-Region
  * there is no automatic Failover
