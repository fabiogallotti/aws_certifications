# Lambda #

## Introduction ##

Let's you run code without provisioning or managing servers. (The so called Serverless functions.) You pay per each invocation, that can be done via SDK or through another AWS resource or third party ones.

The code is executed only when needed, and scales automatically from a few to 1000 lambda functions, in seconds.

## Main Concepts ##

* **Pricing**:
  * The first 1 million requests per month are free, then $0,20 per 1 million requests.
  * The first 400.000 Gb/second per month are free, then $0,000016667 per each Gb/second
  * Pay per invocation, duration times amount of memory

* **Limits**:
  * max 1000 Lambda running concurrently
  * you can store temporary files in a Lambda up to 500 Mb
  * run in No VPC to have internet access
  * timeout max 15 minutes (if you need more, consider **Fargate**)
  * memory can be set between 128 Mb to max 3008 Mb, increments of 64 Mb

* **Cold Starts**:
  * Lambdas have servers preconfigured, that needs to be turned on when invoked. There could be a delay, called **Cold Start**
  * If you invoke again the Lambda while the server is still running, there will be only a little delay. This is a **Warm Server**
  * Serverless functions are cheap, but can have delays in the User Experience
  * There are strategies such as **Pre Warming** that can reduce Cold Starts, keeping the servers continuously running

* **Functions Version**
  * it's versioning for Lambda
  * each version has it's unique ARN (Amazon Resource Name)
  * the current version is labelled $LATEST
  * you can have two types of ARN:
    * **Qualified**
      * you specify the version suffix
      * you can create Aliases
    * **Unqualified**
      * without version suffix
      * always points to the latest
      * you cannot use Aliases

* **Aliases**, allows you to give friendlier name to a specific version, when working programmatically

* **Layer**, it's a ZIP archive that contains libraries, custom runtime and dependencies. You can use them without the need to include them in the deployment package
  * max 5 layers attached to a function
  * all layers can't the unzipped size of 250 Mb
