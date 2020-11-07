# Route 53 #

## Introduction ##

It's an highly available and scalable cloud Domain Name System (DNS).

You can:

* register and manage domains
* create various records set on a domain
* implement complex traffic flows (blue/green)
* continuously monitor records via health checks
* resolve VPC's outside AWS

## Core Concepts ##

* **Traffic Flow**, it's a visual editor that let's you create sophisticated routing configurations; it supports versioning. It costs $50/month per policy record
* **Record Sets**, they allow to point our naked domains and subdomains via Domain records. (send *www* to a specific IP). You can use an **Alias** when routing traffic to AWS, so you can specify a specific resource. It detects IP changes and adjust automatically
* **Routing Policies**, there are 7 types:
  1) **Simple**, one record and multiple IP addresses. When multiple values are specified, Route53 will return all IPs in a random order
  2) **Weighted**, split traffic based on weights assigned
  3) **Latency-Bases**, direct traffic based on the lowest newtork latency for the end-user, based on the region
  4) **Failover**, create active/passive setups in situations where you have a primary site in one location and a secondary one in another. If an endpoint of the primary is unhealthy, the traffic goes to the secondary
  5) **Geolocation**, direct traffic based on the geographic location of where the request originated from
  6) **Geo-proximity**, direct traffic based on the geographic location of the user and the AWS resource. You can route more or less traffic to a specific resource using a Bias. (**You need to use Traffic Flow**)
  7) **Multi-value Answer**, return multiple values such as IPs for response to DNS queries. It performs health checks automatically and only returns healthy values (it's the Simple + health checks)
* **Health Checks**
  * Every 30s by default, can be reduced to 10s
  * Can initiate a failover if the status is unhealthy
  * A CloudWatch Alarm can be created to alert for unhealthy state
  * An Health Check can monitor other Health Checks to create a chain of reactions
* **Resolver**, a regional service that lets you route DNS queries between your AWS VPCs and your On-Premise network (tool for **Hybrid Environments**)
