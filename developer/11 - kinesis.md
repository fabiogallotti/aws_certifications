# Kinesis #

## Introduction ##

It's a scalable and durable real-time data streaming service to ingest and analyze data from multiple sources. It collects, processes and analyzes streaming data, in **real-time**.

It's a solution for collecting, processing and analyzing streaming data, in real-time.

4 types:

* **Data Stream**
  * Ingests data and stores them into **Shards**
  * Can have multiple consumers, to be manually configured; they are EC2 instances that then send data to some service
  * Pay for running Shards
  * Data can persist from 24 hours (default) to 168 hours
* **Data Firehose**
  * Data immediately disappears after being consumed, they are not persisted
  * You can choose only one consumer from a predefined list
  * Can convert incoming data to few file formats
  * Can compress and secure data
  * Pay for data that is ingested
* **Video Stream**
  * Ingest audio and video data, encoded
  * It will secure and retain those data
  * Output will be consumed by ML or video processing systems
* **Data Analytics**
  * It has an **Input Stream** and an **Output Stream**, that can be Data Stream or Firehose
  * Can run custom SQL query on data that pass through it, and provide results as outputs
  * Real-Time analytics on data (can be expensive)
