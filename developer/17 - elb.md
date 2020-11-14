# Elastic Load Balancer #

## Introduction ##

It distributes incoming traffic across multiple targets. Can be a physical hardware or virtual software that accepts incoming traffic, and then distributes it to multiple targets. The load can be balanced via different rules.

It must have at least two Availability Zones, and cannot be cross-region.

Three types:

* **Application** LB
  * Designed for HTTP/S traffic
  * Layer 7 (Application)
  * Has a feature called **Request Routing** which allows to add routing rules to listeners based on HTTP protocol.
  * A Web Application Firewall (WAF) can be attached to it
* **Network** LB
  * Designed for TCP/UDP traffic
  * Layer 4 (Transport)
  * Can handle millions of requests per second, with low latency
  * Can perform **Cross-zone** balancing
* **Classic** LB
  * It's the legacy Load Balancer
  * Can balance HTTP/S and TCP, but not at the same time
  * Both Layer 4 and 7
  * Can perform **Cross-zone** balancing
  * Will respond 504 error (timeout) if the underlying app is not responding

## Main Concepts ##

* **Listeners**, evaluate any traffic that matches their port
* **Rules**, are invoked by the listeners to decide what to do with traffic. Generally the next step is forward to a Target Group
* **Target Group**, EC2 instances that are registered as target

  * For ALB or NLB, the traffic is sent to listeners. When the port matches, the listener check the rules to decide what to do. The rule will forward the traffic to a target group, that will evenly distribute the traffic to the instances inside the group.
  * For CLB, the traffic is sent to listeners, and when the port matches, the traffic is directly sent to any EC2 instance that is registered to it. You cannot apply rules to a CLB.

* **Sticky Session**, it's an advanced load balancing method, that allows to bind a user's session to a specific EC2 instance.
  * Ensure all the requests from that session are sent to the same instance. Cookies are used to remember the EC2
  * Typically used with CLB, can be enabled for ALB, for a specific Target Group, not for a single EC2 instance
  * Useful when specific info are only stored on a single instance

* **X-Forwarded-For (XFF) Header**, used to check the IPv4 address of a user. It's a command method used for identifying the originating IP of a client, instead of getting the LB address

* **Health Checks**, instances monitored by the ELB report back statuses as *InService* or *OutOfService*. The ELB doesn't terminate unhealthy instances, it will only redirect traffic to the healthy ones.

* **Cross-Zone Load Balancing**, available only for Classic and Network LB
  * if Enabled, requests are distributed evenly across instances **in all** enabled AZ
  * if Disabled, requests are distributed evenly across instances **in only** it's AZ

* **Request Routing**, it's an Application LB specific feature, for applying rules to incoming requests and then forward or redirect traffic
