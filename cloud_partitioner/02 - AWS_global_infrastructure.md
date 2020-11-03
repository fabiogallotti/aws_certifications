# AWS Global Infrastructure #

Where does all this Cloud Computing Run?

- 69 **Availability Zones** (one or more data centers), within 22 **Geographical Regions** (physical location in the world with multiple AZ inside) around the world.
- A lot more **Edge Locations** (data centers owned by partners of AWS).

The infrastructure is steadily expanding.

## Regions ##

- A **geophically distinct** location, which has multiple datacenters (Availability Zones);
- Every region is **physically isolated**, independent from the others;
- Each region has at **least two** AZs;
- Not all AWS services are available in all regions;
- *us-east-1* (North Virginia) is the region with the billing info.

## Availability Zone ##

- It's a datacenter owned and operated by AWS, where AWS services run;
- Each region has at least two AZs;
- Represented by a region code, followed by a letter identifier (*us-east-1a*);
- The latency between AZs is <10ms;
- **Multi-AZ** = distributing your instances across multiple AZs allows failover configuration for handling requests when one goes down.

## Edge Locations ##

- It's a datacenter owned by a trusted partner of AWS, which has direct connection to the AWS network;
- Serve requests for **CloundFront** and **Route 53**;
- **S3 Transfer Acceleration** traffic and **API Gateway** endpoints also uses the Edge Network;
- Allow **low latency** no matter the geographical location of the end user.

## GovCloud Regions ##

- Allow customer to host sensitive Controlled Unclassified Information. Are only operated on U.S. soil by U.S. citizens, and accessible by U.S. entities.
