# Step Functions #

## Introduction ##

Allow to coordinate multiple AWS services into serverless workflows. It's creating a state-machine with microservices.

* **State-Machine**, is an abstract model which decides how one state moves to another one, based on a series of conditions. Step functions has two types of them:
  * **Standard**, for general purpose, long workloads
  * **Express**, for streaming data, short workloads

**Main features**:

* automatically triggers and tracks each step
* automatically retries in case of error
* logs the state of each step
* it has a graphical console to visualize the components of an app, as a series of steps
* can execute steps in parallel
* **States** configured using JSON language, are:
  * **Pass**, passes its input to its output, without doing any work
    * **Parameters**, key-value pairs passed as input
    * **Result**, virtual task to be passed to the next state
    * **ResultPath**, where to put the output of the virtual task
  * **Task**, represents a single unit of work. Can be performed by:
    * a Lambda function
    * passing parameters to the API action of other AWS services
    * using an **activity**, that means that the work can be hosted anywhere, even outside AWS
  * **Choice**, adds branching logic
  * **Wait**, delays for a specified time
  * **Succeeded**, stops an execution successfully
  * **Fail**, stops an execution marking it as failure
  * **Parallel**, allows to create parallel branches of execution, and the state machine doesn't move forward until both branches complete
  * **Map**, allows to execute the same step for multiple entries of an array in the state input
