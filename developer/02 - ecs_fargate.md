# Elastic Container Service (ECS) vs Fargate #

## ECS ##

It's a fully managed container orchestration service. It's an highly secure, durable and scalable way to run containers.

## ECS Components ##

* **Cluster**, multiple EC2 instances that will host the docker containers
* **Task Definition**, a json file that defines the configuration of up to 10 containers you want to run (you need to have one **essential** container)
* **Task**, launches containers defined in a task definition. It's a container that runs only for the duration of a workload
* **Service**, it's a long running task
* **Container Agent**, it's a binary on an EC2 instance, which monitors, starts and stops tasks.

## Elastic Container Registry (ECR) ##

It's a Docker repository where you can store, manage and deploy Docker images.

## Fargate ##

To run **serverless** containers, paying based on usage and consumption.

* You can create an empty cluster, and then launch a Task as **Fargate**.
* No longer have to provision, configure and scale a cluster of EC2 instances
* Charged for at least one minute and then by seconds

Configuration of a Fargate Task:

* Define the total **memory** and **vCPU** in the Task Definition
* Add your containers and allocate the memory and vCPU for each of them
* When running the task you can choose the VPC and subnet it will run in

**Notes**:

* You can apply a **Security Group** and an **IAM role** to a Task or a Service, both for **ECS** and **Fargate**
* Fargate and Lambda seems similar, but there are key differences:
  * duration (Fargate unlimited, Lambda max 15 mins)
  * memory (Fargate up to 30GB, Lambda 3GB)
  * containers (Fargate personalized, Lambda standardized)
  * pricing
