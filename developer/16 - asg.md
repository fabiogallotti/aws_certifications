# Auto Scaling Group (ASG) #

## Introduction ##

It sets scaling rules which will automatically launch additional EC2 instances or shutdown some, to meet the current demand.

* Contains a collection of EC2 instances that are treated as a group in the scope of scaling and management.
* Automatic scaling can occur via
  * **Capacity Settings**
    * Size of the ASG is based on Min, Max and Desired capacity
    * Min = how many instances should **at least** be running
    * Max = maximum number of instances allowed
    * Desired = how many instances you want to ideally run
  * **Health Check Replacements**
    * EC2 status check, if the instance is unhealthy it will be stopped and a new one launched
    * ELB health check, it's a ping to an HTTPS endpoint, with expected response.
  * **Scaling Policies** (scaling out = adding, scaling in = removing)
    * **Target Tracking**, maintains a specific metric at a target value (Average CPU utilization < 75%)
    * **Simple**, when an alarm is breached, scale
    * **With Steps**, scales when alarm in breached and can scale based on alarm value changing

* Can be associated with an ELB, to have richer health checks
  * Classic LB, associated **directly** to the ASG
  * Application and Network LB, associated **indirectly** via their Target Groups

* **Launch Configuration** is a configuration template for an instance, that an ASG can use to launch EC2 instances.
  * cannot be edited, if you want to update it you need to create a new one
  * **Launch Template** is a LC with versioning
