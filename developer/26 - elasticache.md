# ElastiCache #

## Introduction ##

It's a managed caching service, used to deploy, run and scale popular, open source compatible, In-Memory Data Stores.

* **Caching**, process of storing data in a temporary storage area, optimized for fast retrieval but with no durability.
* **In-Memory Data Store**, like RAM, the data is stored in-memory. High volability but access really fast.

## Properties ##

* only accessible to resources operating with the same VPC, to ensure low latency
* frequently, identical queries are stored in the cache
* supports:
  * **Redis**
    * can perform many operations on the data
    * good for leaderboards
    * fast but less than Memcached (arguable)
  * **Memcached**
    * preferred for caching HTML fragments
    * it's a simple key-value store
    * very fast
