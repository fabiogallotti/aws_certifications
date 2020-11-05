# Security #

## Shared Responsibility Model ##

Customers are responsible for the security **IN** the cloud.

* Data in the cloud
* Configurations

AWS is responsible for the security **OF** the cloud.

* Hardware and Global Infrastructure
* Operation of Managed Systems

## AWS Compliance Programs ##

A set of internal policies and procedures to comply with laws, rules, regulations, or to uphold business reputation.

* **HIPAA** = *Health Insurance Portability and Accountability Act*, U.S. legislation that provides data privacy for safeguarding medical information
* **PCI DSS** = *Payment Card Industry Data Security Standard*, when you want to sell things online and you need to handle credit card information

## AWS Artifact ##

How do we prove that AWS meets a compliance?

It's a no cost, self-service portal for on-demand access to AWS' security and compliance reports (*Artifacts*).
It contains a checklist explaining how are they meeting the requirements, based on a global compliance framework.

The Artifact is a PDF with an XLSX inside (you can use only Acrobat Reader to read it).

## Amazon Inspector ##

**Hardening** = the act of eliminating as many security risks as possible.

How do we prove that an EC2 instance is harden?

AWS Inspector runs a security benchmark against a EC2 instance. You can run a variety of security benchmarks.

Can perform both Network and Host Assessments.

One very popular benchmark is run by CIS (Center for Internet Security), and it has 699 checks.

## AWS Web Application Firewall (WAF) ##

It protects your web application from common web exploits.

You can write your own rule to *Allow* or *Deny* traffic based on the HTTP request contents or use a ruleset from a trusted AWS Security Partner.

WAF can be attached to either CloudFront or a Load Balancer.

It protects from the OWASP (Open Web Application Security Project) Top 10 most dangerous attacks:

1) Injection
2) Broken Authentication
3) Sensitive data exposure
4) XML External Entities (XXE)
5) Broken Access Control
6) Security misconfiguration
7) Cross Site Scripting (XSS)
8) Insecure Deserialization
9) Using Components with known vulnerabilities
10) Insufficient Logging and monitoring

## AWS Shield ##

It's a managed DDoS (Distribute Denial of Service) protection service that safeguard apps running on AWS.

**DDoS Attack** =  a malicious attempt to disrupt the normal traffic by flooding a website with a large amount of fake traffic.

All customers benefit from AWS Shield Standard, at no additional charge. When you route your traffic through **Route 53** or **CloudFront** you are using the protection.

* **Standard**, Free, protection against the most common attacks, access to tools and best practises; available on *all* AWS services
* **Advanced**, $3.000/year, additional protection against larger attacks, visibility reports, 24/7 support; available on *Route 53*, *CloudFront*, *Load Balancer*, *Elastic IP*

## Penetration Testing ##

It's an authorized simulated cyberattack on a computer system, performed to evaluate the security of it.

You can do Pen Testing on AWS, with some limitations.

**Permitted** Services to Pen Test:

* EC2 instances, NAT gateways, ELB
* RDS, Aurora
* CloudFront
* API Gateways
* AWS Lambda
* Elastic Beanstalk

**Prohibited** Activities:

* DDoS
* Port flooding
* Protocol flooding
* Request flooding

For Other Simulated Events you can submit a request and get a response in 7 days.

## GuardDuty ##

* **IDS** = Intrusion Detection System
* **IPS** = Intrusion Protection System

It's an IDS/IPS service, a threat detection service that continuously monitors for malicious, suspicious activity and unauthorized behaviours. It uses ML to analyze the AWS Logs from CloudTrail, VPC Flow and DNS.

It will alert you of Findings, and you can automate a incident response via CloudWatch Events.

## Key Management Service (KMS) ##

It's a managed service that makes it easy to create and control the encryption keys used to encrypt your data.

It's a Multi-Tenant HSM (hardware security module), and many AWS services are integrated to use it with a simple checkbox.

It uses **Envelope Encryption** = when you encrypt your data, your data is protected, but you have to protect the encryption key; so you encrypt also the key with a master key, adding an additional layer of security.

## Amazon Macie ##

It's a service that continuously monitors S3 data access activity for anomalies, and generates alert when it detects risks of data leaks or unauthorized access.

It analyses CloudTrail Logs. It has a variety of alerts, and can identify the most-at-risk users which could lead to a compromise.

## Security Groups vs Network Access Control Lists ##

* **Security Group** act as a firewall at the instance level. Implicitly denies all traffic, and you need to create rules to Allow it. (Allow a port)

* **NACL** act as a firewall at the subnet level. You can create Allow or Deny rules for traffic. (Block an IP)

## AWS VPN (Virtual Private Network) ##

Let's you establish a secure and private tunnel from your network to the AWS network.

* **Site-to-Site** VPN, securely connects on-premises network to AWS network (entire office)
* **Client** VPN, securely connects user to AWS network (work from home for 1 user)
