# CloudFormation #

## Introduction ##

It's a templating language that defines AWS resources to be provisioned, so it automates the creation of resources via code. (Infrastructure as Code)

## Main Concepts ##

* **Infrastructure as Code**, it's the process of managing and provisioning data centers via definition files (YAML or JSON for CloudFormation) rather than manual configuration
* CloudFormation **Template** sections are:
  * **MetaData**, additional information
  * **Description**, a description about the template
  * **Parameters**, values to pass at runtime
  * **Mappings**, a lookup table
  * **Conditions**, resources created or properties assigned
  * **Transform**, applies macros
  * **Resources**, resource you want to create (at least one)
  * **Outputs**, values returned
* **AWS Quick-Starts** are example templates, pre-built
* **Stack Updates**, when you need to make a change in a stack instead of deleting and recreating it. You can modify the template and push a stack update; CloudFormation will change the resources intelligently
  * Two ways to update:
    * **Direct**, update a template and it will be immediately deployed
    * **Change sets**, you can preview the changes and then decide to apply or not
  * Depending on the state of the resources, the update can be of three types:
    * **Update with no Interruption**, without disrupting operations and without changing resource's physical ID or ARN (Amazon Resource Name)
    * **Update with some Interruption**, there could be some interruption, but no change in the physical ID
    * **Replacement**, recreates the resource during the update, with new physical ID
  * You may want to not update certain resources. This way you can prevent data loss or interruption of service. You can do it creating a **Stack Policy**
    * It's a JSON document that defines the update actions that can be performed (Allow, Deny)
  * **Nested Stacks**, allows you to reference CloudFormation templates inside another one. Advantages:
    * modularity, so reusability
    * reduce complexity using multiple templates
  * **Drift Detection**, is a feature to detected drifts in the configuration. Drift is when the stack actual configuration differs from the template. It happens when developers start to make ad-hoc changes, instead of updating the template.
  * **Rollbacks**, when you create, update or destroy a stack, you could encounter an error. In this case CloudFormation will attempt to rollback to the previous state. Rollbacks are enabled by default, and they can fail as well.
  * **Pseudo Parameters**, are predefined by AWS, you don't declare them in the template (AWS::Region, AWS::StackId)
  * **Resource Attributes**, are additional checks that you can define in the template.
    * **Creation Policy**, prevents its status from reaching creation completed before CloudFormation receives a specified number of success signals
    * **Deletion Policy**, reserves or backups a resource when its stack is deleted (*Delete*, *Retain*, *Snapshot*)
    * **Update Policy**, how to handle updates for ASG, ElastiCache, Domain, Lambda Alias
    * **Update Delete Policy**, retain or backup the existing physical instance when it's replaced during an update (*Delete*, *Retain*, *Snapshot*)
    * **Depends On**, resource is created only after the creation of another one
  * **Intrinsic Functions**, used to assign values to properties that are not available until runtime
    * **Fn::GetAtt**, returns the value of an attribute from a resource in the template
    * **Ref**, returns the value of the specified parameter or resource
  * **Wait Conditions**, similar to Creation Policy, but in this case you wait for an external condition. Used in two cases:
    * coordinate stack resources creation with configuration actions that are external to the stack
    * track the status of a configuration process

## Cloud Development Kit (CDK) ##

Write Infrastructure as Code using an imperative programming language.

* **Transpiler**, turns one source code into another. CDK transpiles into CloudFormation templates.
* **Imperative**, implicits what resources will be created. More flexible, Less certain, Less written (CDK)
* **Declarative**, explicits what resources will be created. Less flexible, More certain, More written (CloudFormation)

## Serverless Application Model (SAM) ##

It's an extension of CloudFormation that lets you define serverless applications. It's both an AWS CLI tool and a CloudFormation Macro.

* **Macro**, it's a replacement output sequence according to a defined procedure. The mapping process that instantiates a macro into a specific sequence is known as **macro expansion**. With macros you are creating a Domain Specific Language (DSL)
  * CloudFormation allows to specify macros through the *Transform* attribute

* **SAM CLI**, makes it easy to deploy, run and package Serverless Applications or Lambdas:
  * `sam local start-api`, runs serverless app locally
  * `sam local start-lambda`, runs lambda locally
  * `sam package`, package an application. Creates a zip and uploads it to S3
  * `sam publish`, publishes your packaged app to AWS Serverless Application Repository
  * `sam validate`, validates a SAM template
