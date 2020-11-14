# Identity Access Management #

## Introduction ##

It manages access to AWS resources and of AWS users.

## Core Concepts ##

* **IAM Identities**
  * **Users**, end users who log into the console or interact programmatically with AWS resources
  * **Groups**, groups of users, that share all the same permissions
  * **Roles**, associates permissions to a role, and then assign the role to Users or Groups
* **IAM Policies**, JSON document which grants permissions for a specific user, group or role, to access services. Policies are attached to IAM identities
  * **Managed**, it's managed by AWWS and you cannot edit it. Labeled with an orange box
  * **Customer Managed Policies**, created by the customer, editable
  * **Inline**, directly attached to a user

  * The structure of a policy is:
    * **Version**, latest is "2012-10-17"
    * **Statement**, container for policy elements:
      * **Sid**, optional way of labeling
      * **Effect**, Allow or Deny
      * **Principal**, account, user or role to which you allow or deny access
      * **Action**, list of actions allowed or denied
      * **Resource**, the resource to which the policy applies
      * **Condition**, optional, circumstances under which the policy applies
  * **Password** policy, to set the minimum requirements of a password, and to rotate passwords after X days for a user

* **Access Keys**, allows users to interact with AWS programmatically via AWS CLI or SDK. Max two Access Key per user.
* **Multi Factor Authentication (MFA)**, can be enabled per user, but the user has to do it manually, an Admin cannot do it. An Admin can only create policies that requires MFA to access resources.
* **Temporary Security Credentials**, like Access Keys, but temporary. Uses the Security Token Service.
  * Useful in scenarios that involve:
    * **Identity Federation**
      * Linking a person's electronic identity and attributes, stored across multiple distinct identity management systems
      * Two types supported
        * **Enterprise** (SAML)
        * **Web** (Amazon, Google, OpenID Connect 2.0)
    * Delegation
    * **Cross-Account Roles**
      * Grant access for users from a different account to service in your account. No need to create a new user for them.
      * You need to create a Role with a policy that grants access to *sts:AssumeRole*
    * IAM roles
  * Can last from 1 minute to 1 hour
  * Are not stored with the user, but are generated dynamically and provided when requested
  * Are the basis for Roles and Identity Federation
* **Security Token Service (STS)**, it's a web service that enables you to request temporary, limited-privilege credentials for IAM users. It'a global service, accessible only programmatically
  * APIs:
    * *AssumeRole*
    * *AssumeRoleWithWebIdentity*, returns a set of temporary security credentials for users who have been authenticated in a mobile or web application with a web identity provider. The developer **first** authenticates with the **web identity**, gets back a Javascript Web Token, and uses it to call the API. STS will return Temporary Credentials if it recognizes the user
