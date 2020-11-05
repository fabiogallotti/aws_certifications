# Variation Study #

## Cloud* services ##

* **CloudFormation**, Infrastructure as Code, to setup services via templating scripts.
* **CloudTrail**, logs all the API calls between AWS services
* **CloudFront**, Content Distribution Network, it creates a cached copy of your website and copies to server located near people
* **CloudWatch**, is a collection of multiple services, *Logs*, *Metrics*, *Events*, *Alarms*, *Dashboard*
* **CloudSearch**, search engine, to add it to a website

## *Connect service ##

* **Direct Connect**, dedicated Fiber Optics connection from on-premise Data Center to AWS
* **Amazon Connect**, Call Center Service

## Elastic Transcoder vs Media Convert ##

* **Elastic Transcoder**, the old way to transcode videos to streaming formats
* **MediaConvert**, the new way, it adds overlay of images, insertion of video clips, extraction of capture data

## Simple Notification Service (SNS) vs Simple Queue Service (SQS) ##

They both Connect apps via Messages.

* **SNS**, it pass along messages.
  * send notification to subscribers of topics via multiple protocol (HTTP, Email, SMS, SQS)
  * used to send **plain text email** which are triggered by another AWS service (billing alarms)
  * can retry in case of failure for HTTPS
  * good for webhooks, simple internal mails, triggering lambda functions
* **SQS**, it queue up messages, with guaranteed delivery
  * places messages into a queue; applications pull this queue using AWS SDK
  * can retain messages for 14 days
  * can send messages in sequential or parallel order
  * can ensure only one message is sent, or delivered at least once
  * good for delayed tasks

## Inspector vs Trusted Advisor ##

* **Inspector**, audits a single EC2 instance, and generates a report from a list of security checks
* **Trusted Advisor**, doesn't generate a PDF report. It gives you an holistic view across multiple services of recommendation and best practises.

## ALB vs NLB vs CLB ##

Three different types of Load Balancers. They can all be attached with Amazon Certification Manager (ACM) SSL certificate (HTTPS).

* **Application**
  * Specialized for Layer 7 (Application)
  * HTTP and HTTPS traffic
  * Routing Rules, so you can have more usability
  * Can attach a WAF
* **Network**
  * Specialized for Layer 4 (Transport)
  * TCP and TLS traffic, where extreme performance is required
  * Capable of handling millions of requests per second with ultra-low latency
  * Optimized for sudden and volatile traffic while using a single static IP address per AZ
* **Classic**
  * The old one, does the job of both the other two, with few features
  * Layer 4 and 7
  * For application build with the EC2-Classic Network
  * Doesn't use Target Groups

## Simple Notification Service (SNS) vs Simple Email Service (SES) ##

They both send Emails.

* **SNS**, internal use cases
  * send notification to subscribers of topics via multiple protocol (HTTP, Email, SMS, SQS)
  * used to send **plain text email** which are triggered by another AWS service (billing alarms)
  * **Topics** and **Subscriptions** are the key points
* **SES**, a cloud based email service
  * send HTML emails, SNS cannot
  * can receive inbound emails
  * can create email templates
  * custom domain name email

## Artifact vs Inspector ##

They both compile out a PDF.

* **Artifact**, generates a security report that is based on global compliance frameworks.
* **Inspector**, run a script to analyse an EC2 instance, generates a report telling which security checks are passed. **Audit tool for EC2 instances**.
