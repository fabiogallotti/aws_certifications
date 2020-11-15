# CloudTrail #

## Introduction ##

It logs API calls between AWS services. Used when you need to know who to blame for something.

It's a service that enables governance, compliance, operational auditing and risk auditing.

Easily identifies which user/account made the calls to AWS:

* **where** = IP address
* **when** = EventTime
* **who** = User
* **what** = Region, Resource, Action

## Main Concepts ##

* **Event History**, a GUI to visualize data collected by CloudTrail for the last 90 days. If you need logging for more than 90 days, you need to create a Trail.
* **Trail**, output on S3, and you need to access them using Amazon Athena (SQL Queries)
  * can be set to log to all regions
  * can be set to log across all accounts in an Organization
  * can Encrypt Logs
  * can ensure integrity with Log File Validation enabled
* CloudTrail can be set to deliver events to CloudWatch, not the other way around
* Two types of **Events** are logged:
  * **Management**
    * turned on by default, can't be turned off
    * tracks configuring security
    * tracks registering devices
    * tracks configuring roles for routing data
    * tracks setting up loggin
  * **Data**
    * turned off by default
    * tracks specific operations for specific AWS services (S3, Lambda)
