# CI/CD #

## Introduction ##

Are automated methodologies to prepare, test, deliver or deploy code into production servers.

* **Continuous Integration**, automating the integration of code changes. Incourages small changes more frequently. Each commit triggers a build that will run tests and help identify issues
* **Continuous Delivery**, automating the preparation of code to be released in production. Deployment is still manual
* **Continuous Deployment**, automation also of the deployment of the changes to production

The AWS services for doing CI/CD are:

* **CodeCommit**, like Github, it's a source control service that hosts secure git-based repositories
  * **Version Control System** it records changes to files over time, so that you can recall specific versions later
  * Features:
    * in scope with many compliance programs
    * repositories are encrypted at rest and at transit
    * can handle lot of files, branches, history
    * no limits in size of the repos
    * keeps repos close to other production resources in AWS
    * IAM can be used to control user access
* **CodeBuild**, like CircleCI, it's a build pipeline to create temporary servers to build and test the code
  * Scales automatically
  * Compiles code, runs unit tests and produces artifacts
  * **buildspec.yml** is a configuration file for the build, and provides the build instructions:
    * specify a Build Environment, that can be managed images by AWS or custom Docker images
    * specify the source code
    * **can be overriden by CLI**
    * properties:
      * **version**, usually 0.2
      * **phases**
        * install
        * pre_build
        * build
        * post_build
      * **artifacts**
* **CodeDeploy**, to deploy artifacts to staging or production.
  * Performs:
    * In-Place deployment
      * app is stopped in each instance of the deployment group
      * latest version is installed, started and validated
      * you can use an ELB to deregister the instance while the deployment is ongoing
      * only EC2 or On-Premises
    * Blue/Green deployment
      * instances are provisioned for replacement (ASG cloned)
      * latest version is installed on the replacement instances, started and validated
      * replacement instance are registered in the ELB
      * original environment is stopped
  * Core Components:
    * **Application**, the unique identifier for the application being deployed
    * **Deployment Group**, set of EC2 or Lambda where the new revision is deployed to
    * **Deployment**, the process and component used to apply a new revision of an application
    * **Deployment Configuration**, set of deployment rules used during the deployment, with success/failure condition included
    * **appspec.yml**, contains the deployment actions that CodeDeploy should execute. The main parts are:
      * OS
      * Source files
      * Permissions
      * the so called **LifeCycle Event Hooks**:
        * Application Stop
        * Before Install
        * After Install
        * Application Start
    * **Revision**, everything required to deploy a new version (appspec.yml, application files, configuration files, executables)
  * You need to install the **CodeDeploy Agent**, so the EC2 can report back to CodeDeploy, and to create a CodeDeploy Service **Role**
* **CodePipeline**, CI/CD pipeline to setup automatic deployments
  * **Pipeline**, what encludes all components
  * **Stage**, it's a step in the pipeline
  * **Action**, does something (pull source code, build, run tests, deploy, invoke a lambda)
  * **Action Group**, several actions grouped together
  * **Artifact**, is a zip file containing the files outputted by an action. It's stored in an S3 bucket.
  * **Stage Transition**, link to the next stage
* **Code Star**, it has templates for getting common application project setup. You get a deployment pipeline, access management and a project dashboard
