# Virtual Private Cloud (VPC) #

## Introduction ##

It provision a logically isolated section of the AWS Cloud, where you can launch AWS resources in a virtual network that you define.

It gives you complete control over your virtual networking environment.

## Key Features ##

* VPCs are Region Specific
* Max 5 VPCs per region
* every region has a default VPC
* max 200 subnets per VPC
* you can use IPv4 Cidr Blocks or IPv6
* some services are free:
  * **VPC** itself
  * **Route Table**
  * **Network Access Control Lists (NACLs)**
  * **Internet Gateway (IGW)**
  * **Security Group**
  * **Public** and **Private** Subnets
  * **VPC Peering**
* some services cost:
  * **NAT Gateway**
  * **VPC Endpoints**
  * **Virtual Private Gateway**
  * **Customer Gateway**
* DNS Hostname is disabled by default (public IP)

## Main Concepts ##

* **Default VPC**, it's in every region, so you can immediately deploy instances.
  * creates a VPC with a size /16 IPv4 Cidr Block (172.31.0.0/16)
  * creates a size /20 default subnet in each AZ
  * creates an Internet Gateway
  * creates a default Security Group
  * creates a default NACL
  * associates the default DHCP option
  * creates a main route table
* **Default Everywhere IP**, 0.0.0.0/0 represents all possible IP addresses.
  * specifying 0.0.0.0/0 in a route table for IGW, means that we are allowing internet access
  * specifying 0.0.0.0/0 in a security group inbound rule, means that we are allowing all traffic from the internet to access the public resources
* **VPC Peering**, allows to connect one VPC to another over a direct network route, using **private IP** addresses
  * instances on a peered VPC behave like they are on the same network
  * you can connect VPCs across regions or different AWS accounts
  * uses a **Star Configuration** (1 central VPC + 4 other)
  * no transitive peering, you need 1 to 1 connection
  * no overlapping Cidr Blocks
* **Route Table**, used to determine where network traffic is directed. Each subnet in the VPC must be associated with a route table: a subnet can be associated to only one route table, but a route table can be associated with multiple subnets
* **Internet Gateway (IGW)**, allows your VPC to access internet.
  * provides target in your VPC route table for internet-routable traffic
  * performs Network Address Translation (NAT) for instances that have been assigned a public IPv4 address
  * to route out to the internet you need to add a route with IGW as target and destination 0.0.0.0/0
* **Bastions/Jumpbox**, are EC2 instances that are security harden. They are designed to help you gain SSH access to EC2 instances that are in a private subnet. **Session Manager** service replace the need of Bastions
* **Direct Connect** is a solution for establish dedicated network connection from On-Premises to AWS. It's a very fast network, that helps reducing network costs and increases the bandwidth throughput
* **VPC Endpoints**, allow you to privately connect your VPC to other AWS services, keeping the traffic inside AWS network
  * Eliminate the need of IGW, NAT device, VPN connection or AWS Direct Connet
  * Instances in VPC does not need a public IP address to communicate
  * Traffic does not leave AWS network
  * It's an horizonally scaled, redundant and highly available VPC component
  * Allows secure communication between instances and services, without adding availability risks or bandwidth constraints
  * Two types:
    * **Interface**, it's an Elastic Network Interface (ENI) with private IP address; serves as entry point for traffic going to a supported service. Powered by AWS PrivateLink. It has a cost
    * **Gateway**, it's a target for a specific route in the route table. Used with S3 and DynamoDB. It's free
