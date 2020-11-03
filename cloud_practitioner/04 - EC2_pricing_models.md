# EC2 Pricing Models #

EC2 has 4 pricing models:

1) **On Demand** (*Least Commitment*):
   - Low cost and flexible
   - Only pay for hour
   - **Use cases**: Short-term, spiky, unpredictable workloads, first time apps
   - Ideal when your workload cannot be interrupted
   - When you launch an EC2 instance, it's by default **On-Demand** pricing. No up-front payment and no long-term commitment, charged by minutes of usage.

2) **Reserved Instances** (**RI**) (Up to 75% savings, *Best Long-Term*):
   - **Use Cases**: Steady state or predictable usage
   - Commit to EC2 over a 1 or 3 years term
   - Can resell unused reserved instances
   - The reduced pricing is based on:

        **Term x Class Offering x Payment Option**

     - *Term*: 1 or 3 years of commitement.
     - *Class Offering*:
        1) Standard, up to 75% savings; cannot change attributes.
        2) Convertible, up to 54% savings; can change attributes if greater of equal in value.
        3) Scheduled, reserved for specific time periods.
     - *Payment Option* (greater the upfront greater the savings):
        1) All Upfront
        2) Partial Upfront
        3) No Upfront
   - RIs can be shared between multiple accounts in the same organization. Unused RIs can be sold on the Marketplace.

3) **Spot** (Up to 90% savings, *Biggest Savings*):
   - Request spare computing capacity
   - Flexible start and end times
   - **Use Cases**: When you can handle interruptions and for non critical background jobs
   - Terminating conditions:
     - Can be terminated by AWS **at any time**
     - If AWS terminate the instance, you **don't get charged** for a partial hour of usage
     - If you terminate the instance, you **will still be charged** for any hour that it ran.

4) **Dedicated** (*Most Expensive*)
   - Dedicated servers
   - Can be on-demand or reserved servers
   - **Use Cases**: When you need a guarantee of isolate hardware
   - Are designed to meet regulatory requirements: you have strict server-bound licensing that won't support multi-tenancy.
     - Multi-tenancy = multiple customers on the same hardware. *Virtual Isolation*
     - Single Tenant = single customer, single hardware. *Physical Isolation*
