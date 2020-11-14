# Security Group and NACL #

## Security Group ##

It's a virtual firewall that controls traffic from and to an EC2 instance.

* Each Security Group contains a set of rules that filter traffic coming into an out of an EC2 instance
* There are no **Deny** rules. All inbound traffic is blocked by default, unless a rule specifically **Allows** it
* All outbound traffic is allowed by default
* Provides security at the Protocol and Port access level
* Multiple instances across multiple subnets can belong to a Security Group
* An instance can belong to multiple Security Groups, and rules are permissive, so if a rule for one SG Allow some traffic, all the SGs will Allow it.
* Maximum 10.000 Security Groups in a Region, default 2500
* Maximum 60 inbound rules and 60 outbound rules for Security Group
* Maximum 16 Security Groups per Elastic Network Interface, default is 5

## Network Access Control List (NACL) ##

It's an optional layer of security that acts as a firewall for controlling traffic in and out of subnets.

* Acts as a virtual firewall at subnets level. Subnets are associated to a NACL, and a subnet can belong to only one NACL.
* When you create a VPC, you get a NACL
* Each NACL has a set of rules that can **allow** or **deny** traffic into and out of subnets
* You can block a specific IP address
* The rule number defines the order of evaluation, from lowest to highest (32.766)
