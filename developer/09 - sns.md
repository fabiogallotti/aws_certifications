# Simple Notification Service (SNS) #

## Introduction ##

Subscribe to and Send notifications via **text email**, webhooks, Lambda, SQS, mobile.

It's an highly available, durable, and secure **pub/sub** messaging service, that enables to decouple microservices, distributed systems and serverless apps.
(Application Integration)

**Pub/Sub** it's the publish-subscribe pattern, commonly implemented in messaging systems:

* the sender (**publisher**) of a message send it to an event bus
* the **event bus** categorizes messages into groups
* the receiver (**subscriber**) subscribes to these groups
* the publisher doesn't know who the subscribers are
* the subscriber doesn't pull messages, but messages are pushed to him

## Core concepts ##

* **Topics**, it's a logical access point and communication channel. It allows to group multiple subscriptions together. It can deliver multiple protocols at once. You can encrypt using KMS
* **Subscriptions**, can only be done to one protocol and one topic. To receive messages from a topic you need to have a subscription to it
* **Protocols**:
  * HTTP/S
  * Email
  * SQS
  * Lambda
  * SMS
* **Application as a Subscription**, send notifications directly to app on your mobile devices (Mobile Push)
