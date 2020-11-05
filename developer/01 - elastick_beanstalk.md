# Elastic Beanstalk (EB) #

## Introduction ##

Used to quickly deploy and manage web-apps on AWS without worrying about the underlying infrastructure. (**PaaS**)

**PaaS** it's a platform allowing to develop, run and manage applications without the complexiy of building and maintaining the infrastructure typically associated with developing and launching an app.

You choose the platform, upload your code and it runs. It's not recommended for Production applications of large companies.

It's powered by a **CloudFormation** template that setups the Elastic Load Balancer, Autoscaling Group, RDS database, EC2 instances preconfigured, Monitoring, In-Place and Blue/Green deployment, Security and Dockerized environments.

## Web vs Worker Environment ##

When you first create an EB application you have choose between *Web* (for web-app) and *Worker* (for background jobs) Environment. You generally create both that communicate between each other.

* **Web**, creates an ASG and an optional ELB
* **Worker**, creates an ASG, an SQS queue, Sqsd daemon on the EC2 instance, CloudWatch alarms to automatically scale

There are two types of **Web** Environments:

* **Load Balanced Env** = uses ASG to scale with an ELB. It's designed to scale
* **Single Instance Env** = uses an ASG with desired capacity of 1, so one server is always running. There is no ELB to save money. It needs a public IP to route the traffic to the server.

## Deployment Policies ##

There are four different **In-Place** Deployment Policies available with Elastic Beanstalk:

* **All at Once**, for Load Balanced and Single Instance
  1) Deploys the new app to all instances at the same time
  2) Takes all the instances **out of service** during the deployment
  3) Services available again after
  * It's the **fastest** but the most **dangerous**
  * **In case of failure**: rollback re-deploying original state
  * Possible Impact = **Downtime**
* **Rolling**, for Load Balanced only
  1) Deploys the new app to a batch of instances at the a time (like 2 out of 4)
  2) Takes the batch instances **out of service** during the deployment
  3) Re-attaches the updated instances
  4) Go to a new batch and repeat
  * **In case of failure**: perform an additional rolling update to rollback changes
  * Possible Impact = single batch out of service
* **Rolling with additional batch**, for Load Balanced only
  1) Launch new instances that will replace a batch
  2) Deploy the new app on the new batch
  3) Attach the new batch and terminate the old one
  * Capacity is never reduced, no availability issues
  * **In case of failure**: perform an additional rolling update to rollback changes
* **Immutable**, for Load Balanced and Single Instance
  1) Create a new ASG with EC2 instances
  2) Deploy the new app on the new ASG
  3) Point the ELB to the new ASG and shutoff the old ASG
  * It's the **safest**
  * **In case of failure**: terminate the new ASG and restart the old one

Rolling requires an ELB, because it attaches and detaches instances in batches from the ELB.

## In-place vs Blue/Green ##

Elastic Beanstalk by default performs **In-Place** updates, but the context can change the meaning of these two methodologies.

* In-Place could mean within the scope of Elastic Beanstalk Environment (*exam will refer to this*)
  * **Immutable**, the ELB is switched inside the EB env, so it's In-Place
  * **Blue/Green**, there is a **DNS swap** between two EB envs, with two ELBs, so it's outside the env. It's used with DB generally, to avoid data loss
* In-Place could mean within the scope of the same server, so the server is not replaced
  * **All at Once**
  * **Rolling**
* In-Place could mean within the scope of an uninterrupted server, so it implements a **Zero Downtime** deployment
  * Blue/Green occurs on the server itself
  * EB **can't** do that

## Configuration Files ##

EB environment can be customized using configuration files, that are in a the *.config* file in the folder called *.ebextensions*, at the root of the project.

You can config:

1) Option Settings
2) Linux / Windows Server Configuration
3) Custom Resources

It's useful if you want to share the configuration of your project.

## Environment Manifest ##

The Environment Manifest is a file called *env.yml* which is stored at the root of the project.

This file allows you to configure the defaults such as:

1) Environment Name
2) Solution Stack
3) Environment Links
4) Defaults Configuration for other AWS services

To specify groups of values you can use a "+" in the end.

## Linux Server Configuration ##

* **Packages**, download and install prepackaged applications and components
* **Groups**, create Linux groups and assign group IDs
* **Users**, create Linux users, that can be assigned to a group
* **Files**, create files on the EC2 instance
* **Commands**, execute commands on the EC2 instance before the app is setup
* **Services**, define which services should be started or stopped when the instance is launched
* **Container Commands**, execute commands that affect your application source code

## EB CLI ##

The CLI is hosted on github (<https://github.com/aws/aws-elastic-beanstalk-cli-setup>), you need to clone it to use it.

* **eb init**, configure the project directory and the EB CLI
* **eb create**, create the env
* **eb status**, see the current status of the env
* **eb health**, view the health info about instances and overall state of the env
* **eb events**, see a list of events output by EB
* **eb logs**, pull logs from an instance in your env
* **eb open**, open the env's website in a browser
* **eb deploy**, once the env is running, deploy an update
* **eb config**, take a look at the configuration options available
* **eb terminate**, terminate the env

## EB Custom Image ##

When you create an EB env, you can specify an Amazon Machine Image (AMI) instead of using the standard one. You can do this to improve provisioning times when instances are launched, and if you need to install lot of software that isn't included in the AMI

## Configuring RDS ##

You can add a DB inside or outside your EB environment.

* **Inside** is generally intended for **development** envs. When the env is terminated, the DB is terminated as well.
* **Outside**, is generally intended for **production** envs. You create the DB first in RDS and configure EB to use it. If EB terminated, the DB is still there.

## Follow Along ##

**Cloud9** is a cloud IDE for writing code in AWS (Run the command `npm i c9 -g`).

**Cidr Block** it's a range of IP addresses.

We can preview an app with Cloud9, but we need to open the Cloud9 ports to the internet before. In the EC2 instance, you can do it adding the port 8080 to the security group. It can be done via the CLI.

* `169.254.169.254` is the local IP address of an EC2 instance
* `curl -s http://169.254.169.254/latest/meta-data/mac` gives you the mac address, that we will use to get the security group id
* `curl -s http://169.254.169.254/latest/meta-data/network/interfaces/macs/<mac_address_found_before>/security_group_id`
* Now let's open the port using AWS CLI:
  * `aws ec2 authorize-security-group-ingress --group_id <group_id> --port 8080 --protocol tcp --cidr <IP>/32`
  * IP got from checkip.amazonaws.com
* To check everything is done correctly:
  * `aws ec2 describe-security-groups --group_ids <group_id> --output text --filters Name=ip-permission.to-port,Values=8080`
* Get the IP of the EC2 instance
  * `curl -s http://169.254.169.254/latest/meta-data/public-ipv4`

We can store the code of the app in Git; if you are using the EB CLI (you need to install it in Cloud9 and add it to the PATH), you will be asked if you want to push the code to **CodeCommit**.

**N.B.**: To have the proper rights on your account, you may need to create a manual sample application before, and then delete it.
