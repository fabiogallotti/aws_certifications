# Amazon Cognito #

## Introduction ##

It's a decentralized way to manage authentication, sign-up, sign-in integration for your apps.

Two main concepts to know:

* **Identity Provider**, trusted provider of user identity that lets you authenticate to access other services:
  * Single Sign On (SAML)
  * OAuth (OIDC)
* **Web Identity Federation**, to exchange identity and security information between an Identity Provider (IdP) and an app

## Main Concepts ##

* **User Pools**, are user directory used to manage sign-up, sign-in, account recovery, account confirmation.
  * A way to decentralize authentication
  * Successful authentication generates a JSON web token
* **Identity Pools**, provide temporary credentials to access AWS services. It's the actual mechanism authorizing access to AWS services
* **Cognito Sync**, syncs user data and preferences across all devices. It uses push synchronization to push updates and sync data; it uses SNS to send notification to all user devices
