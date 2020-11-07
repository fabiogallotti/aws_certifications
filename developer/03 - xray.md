# X-Ray #

## Introduction ##

Helps analyze and debug applications utilizing microservice architecture.

It's a *Distributed Tracing System*, or a *Performance Monitoring System*.

* **Microservice architecture** is an architectural and organizational approach to software where you have small components, independent services, that communicate over APIs. They are easy to scale, and fast to develop
* **Distributed Tracing**, method used to profile and monitor apps, especially microservices. It helps pinpoint where **failures** occur and what causes **poor performances**
* **Performance Monitoring**, detect and diagnose complex applications performance problems, to maintain an expected level of service

**X-Ray** is a *Distributed Tracing System*, that collects data about requests served by your applications and filters data to identify issues and way for optimization.

**X-Ray** integrates with Lambda, API Gateway, ELB, SNS, SQS, EB, Fargate, ECS, EC2; it supportes Python, Go, Java, Node.js, Ruby, PHP, .NET

The **X-Ray SDK** provides:

* **interceptors** to be added in your code to trace HTTP requests
* **client handlers** to instrument clients that your app uses to call other AWS services
* **HTTP client** to instrument other internal/external web services

**Instrumentation** means the ability to monitor or measure the level of a product's performance, to diagnose errors and to write trace info

## Main Concepts ##

* X-Ray **Daemon**:
  * Instead of sending traffic data directly to **X-Ray**, the SDK sends JSON segment documents to a daemon, listening for traffic.
  * The daemon buffers the segments into a queue and uploads them to X-Ray in batches.
* X-Ray receives data from services as **Segments**
* X-Ray groups segments that have a common request in **Traces**
* X-Ray processes traces to generate a **Service Graph** that provides a visual representation of the app.

## Details ##

* **Segment**, data about the compute resource that is running the app. Info about host, request type, response status, work done, issues
* **Subsegment**, provide more granular timing info and details about downstream call that the app makes. You can define arbitrary subsegments, with the SKD **start** and **end**
* **Service Graph**, it's a flow chart visualization shows the client, frontend services, backend services. It helps identify bottlenecks, latency spikes, issues
* **Trace**, collects all segments generated by a single request. A **Trace ID** tracks the path of a request. It's the first service that adds the Trace ID and propagates it
* **Sampling**, not all the requests get recorded. By default, X-Ray SDK records the **first request each second** and **5% of any additional** request. It helps saving money, reducing the amount of traces recorded
* **Trace Header**, all requests are trace up to a minimum, after that only a percentage is traced. The first service adds a Tracing Header. Then it can have a parent ID if it's propagated
* **Filter Expressions**, with large applications, sampling is not enough. With **Filter Exp** you can narrow down to specific paths or users. Can group the result as well
* **Groups**, you can assing a **Filter Exp** to a group. Updating a group Filter Exp doesn't change the history, but only the new traces
* **Annotations and Metadata**, other info that are aggregated at trace level, and can be added to segments and subsegments.
  * **Annotations** = Key-Value pairs that are **indexed** (for search), with a limit of 50
  * **Metadata** = Key-Value pairs that are **not-indexed** (not for search)
* **Exceptions**, SKD records exception details and stack traces.