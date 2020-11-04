# Billing and Pricing #

## Free Services ##

Completely free:

* **IAM**, Identity Access Management
* **Amazon VPC**, Virtual Private Cloud
* **AWS Cost Explorer**

Free, but they can provision AWS services that have a cost:
* **Auto Scaling**
* **CloudFormation**
* **Elastic Beanstalk**

## Support Plans ##

AWS has 4 different Support Plans to help you.

1) Basic = **$0/month**
   * Email support only, for Billing and Account
   * 7 Trusted Advisor Checks
2) Developer = **$20/month**
   * Tech support via Email (~24h to reply)
   * **No** third party support
   * **Yes** General Guidance (<24h) and System Impaired (<12h)
   * 7 Trusted Advisor Checks
3) Business = **$100/month**
   * Tech support via Chat, Phone Anytime 24/7
   * Fast support for Production System
     * Impaired <4h
     * Down <1h
   * **Yes** third party support
   * All Trusted Advisor Checks
4) Enterprise = **$15.000/month**
   * All the Business plus **Two** dedicated people, a *Personal Concierge* and a *Technical Account Manager* (TAM)
   * Response time <15 minutes for Production issues
   * All Trusted Advisor Checks

## AWS Marketplace ##

It's a digital catalogue with thousands of software listing from independent software vendors (software that already runs with AWS).

The products can be free to use or have an associated charge, that becomes part of your AWS bill, and the AWS Marketplace pays the provider.

The sales channel allow to sell your solutions to other AWS customers.

## AWS Trusted Advisor ##

Advises you on **security**, **saving money**, **performance**, **service limits** and **fault tolerance**. (Like an automated checklist of best practises)

*All Support Plans* = **7 Free** Trusted Advisor Checks

*Business* and *Enterprise* = **All** Trusted Advisor Checks

There are 5 different categories where it can advise you on:
1) **Cost Optimization**, checks: Idle Load Balancers, Unassociated Elastic IP addresses
2) **Performance**, checks: High Utilization of EC2 instances
3) **Security**, checks: MFA on Root Account, IAM Access Key Rotation
4) **Fault Tolerance**, checks: RDS backups
5) **Service Limits**, checks: VPC

## Consolidated Billing ##

One bill for all your accounts.

Allows you to consolidate into one bill, the billing and payments methods across multiple AWS accounts. There is no additional cost on using it.

You can designate a master account in your organization that pays the charges of all the member accounts.

**Cost Explorer** allows you to visualize usage of consolidated billing.

**Volume Discounts** = the more you use, the more you save. Consolidated billing let you take advantage of this because you consolidate the usage of all.

## AWS Cost Explorer ##

Let's you visualize, understand and manage your AWS costs and usage over time.

With multiple accounts within an AWS organization, all the costs will be consolidated in the master account.

You have default reports and you can try to forecast, view data at different level of granularity (monthly, daily), filter data and grouping them.

## AWS Budgets ##

It helps plan your **service usage**, **service costs** and **Instance reservation**.

The first **two** budgets are free, then each one costs $0.02/day, with a limit of 20.000 budgets.

You can setup alerts if you exceed or are approaching the predefined budget.

Budgets can be on **Costs**, **Usage** or **Reservation**, and they can be tracked monthly, quarterly or yearly, with customizable start/end dates.

Alerts support EC2, RDS, Redshift, ElastiCache reservations.

You get notified by providing an Email or Chatbot, and a threshold.

## Total Cost of Ownership (TCO) Calculator ##

Allows you to estimate how much would you save when moving to AWS from On-Premise.

Provides a detailed set of reports, and it's build on underlying calculation models that generates fair assessments of the value you can achieve.

It's for **approximations only**.

## AWS Landing Zone ##

It helps Enterprises to quickly setup a secure AWS multi-account. Provides a baseline environment to get started with a multi-account architecture.

It works through **Account Vending Machine** (AVM), that automatically provision and configure new accounts via the Service Catalog Template, and uses Single Sign-On (SSO) for managing and accessing accounts.

The environment is then customizable to allow customers to implement their own account baselines through a Landing Zone configuration, and update the pipeline.

## Resource Groups and Tagging ##

**Tags** = word or phrases that act as metadata for organizing AWS resources.

**Resource Groups** = collection of resources that share one or more tags. Can display details about a group, based on *Metrics*, *Alarms* or *Configuration Settings*.
You can change at any time the settings to change which resources appear.

They help you organize and consolidate information based on your project and the resources you use.

## AWS Quick Start ##

Set of prebuilt templates by AWS and AWS partners to help you deploy popular stacks on AWS.

Reduce hundreds of manual procedures into just few steps.

A **Quick Start** is composed of 3 parts:
1) a reference architecture for deployment
2) AWS CloudFormation templates that automate and configure the deployment
3) A deployment guide explaining the architecture and implementation in details.

## AWS Cost and Usage Report ##

It generates a detailed spreadsheet, enabling a better analysis and understanding of the AWS costs.

It places the reports into **S3**, uses **Athena** to turn the report into a queryable DB, uses **QuickSight** to visualize the data as graphs.
