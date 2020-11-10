# Parameter Store & Secrets Manager #

## Parameter Store ##

It's a secure, hierarchical storage for configuration data management and secrets management.

You can store password, database strings, licence codes as parameter values.

You can group parameters together with naming convention, by using forward slashes.

The **Type** of the parameter can be:

* String, simple string
* StringList, comma separated string
* SecureString, encrypted with KMS

There are two **Tiers**:

* **Standard**, 10.000 parameters/region, Free, 4 Kb max, No Parameter Policies
* **Advanced**, 100.000 parameters/region, 5 cents parameter/month, 8 Kb max, Yes Parameter Policies

You can convert a standard parameter to advanced, but not the opposite (avoiding data loss).

**Parameter Policies** are a feature available only for the Advanced Tier.

* Helpful in forcing you to update or delete passwords
* It uses asynchronous, periodic scans
* After one policy is created, no additional actions have to be done to enforce it
* You can apply multiple policies to a single parameter
* Three types:
  * **Expiration**, policy deletes a parameter after a specific date or time
  * **ExpirationNotification**, policy triggers an event in CloudWatch that notifies after the upcoming expiration
  * **NoChangeNotification**, event in CloudWatch if a parameter has not been modified for a specific amount of time

## Secrets Manager ##

It's used to protect secrets needed to access your application and services. It can easily rotate, manage and retrieve DB credentials, API keys and other secrets.

It's mostly used to store and rotate DB credentials. (RDS, Redshift, DocumentDB, generic DB, Key/Value)

It enforces encryption using KMS.

Pricing is 40 cents per secret per month, and 5 cents per 10.000 API calls.

CloudTrail can monitor credentials access in case you need to audit.

A huge value is the **Automatic Rotation**, that can be setup for any DB credentials, and it's performed via a Lambda function.
