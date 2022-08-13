# Introduction to Configuration as Code

AWS CloudFormation leverages standard AWS APIs to provision and update infra- structure in your account. Though AWS
CloudFormation is highly effective at this task, there are some configuration tasks that are either inaccessible from
the AWS API or more easily done with standard configuration management tools, such as Chef and Puppet.

AWS OpsWorks Stacks provides a serverless Chef infrastructure to configure servers with Chef code, known as recipes.

Amazon Elastic Container Service (Amazon ECS) allows you to define the requirements of, schedule, and configure Docker
containers to deploy to a cluster of Amazon EC2 instances.

# Using AWS OpsWorks Stacks to Deploy Applications

AWS OpsWorks Stacks is the only service that performs configuration management tasks.

Configuration management is the process designed to ensure that infrastructure in a given system adheres to a specific
set of standards, settings, or attributes.

Popular configuration management tools include Chef and Puppet. AWS OpsWorks Stacks allows you to manage the
configuration of both on-premises and cloud infrastructures.

There are two additional AWS OpsWorks services, AWS OpsWorks for Chef Automate and AWS OpsWorks for Puppet Enterprise.

# AWS OpsWorks Stack Concepts

## Cookbooks and Recipes

Chef is a Ruby-based configuration management language that AWS OpsWorks Stacks uses to enforce configuration on Amazon
EC2 on-premises instance nodes.

Chef uses a declarative syntax to describe how to configure a node without detailing the actual steps to achieve the
desired configuration.

## Stack

A typical workload in AWS will include systems for various purposes, such as load balancers, application servers, proxy
servers, databases, and more. The set of Amazon EC2 on-premises instances, Amazon RDS, Elastic Load Balancing, and other
systems make up a stack. You can organize stacks across an enterprise.

Stack Name identifies stacks in the AWS OpsWorks Stacks console. Since this name is not unique, AWS OpsWorks assigns a
Globally Unique Identifier (GUID) to the stack after you create it.

AWS OpsWorks associates a stack with either a global endpoint or one of multiple regional endpoints. When you create a
resource in the stack, such as an instance, it is available only from the endpoint you specify when you create the
stack.

Stacks can create and manage instances in Amazon EC2 Classic or an Amazon Virtual Private Cloud (Amazon VPC). When you
select an Amazon VPC, you will be able to specify in what subnets to deploy instances when they are created.

## Layer

A layer acts as a subset of instances or resources in a stack. Layers act as groups of instances or resources based on a
common function. This is especially important, as the Chef recipe code applies to a layer and all instances in a layer.

After a layer is created, any elastic load balancers in the same region associate with the layer.

You can configure layers to assign public or elastic IP addresses to instances when they come online.

Amazon RDS layers pass connection information to an existing Amazon RDS instance. When you associate an Amazon RDS
instance to a stack, it is assigned to an app. This passes the connection information to the instances via the app’s
deploy attributes, and you can access the data within your Chef recipes with node.

Amazon ECS cluster layers provide configuration management capabilities to Linux instances in your Amazon ECS cluster.
You can associate a single cluster with a single stack at a time.

## Instances

An instance represents either an Amazon EC2 or on-premises instance, and the configuration AWS OpsWorks Stacks
enforces upon it.

An instance represents either an Amazon EC2 or on-premises instance, and the configuration AWS OpsWorks Stacks
enforces upon it.

AWS OpsWorks Stacks supports three instance types.

**24/7 instances** This instance type runs until you manually stop it.

**Time-based instances** Instances of this type run on a daily and weekly schedule that you configure and are useful for
handling predictable changes in a load on your stack.

**Load-based instances** Load-based instances start and stop automatically based on metrics such as NetworkOut or
CPUUtilization.

When you create an Amazon EC2 instance, you have the option to choose either the instance-store or Amazon EBS backed
instance types.

## Apps

An app refers to the location where you store application code and other files. This can be an Amazon S3 bucket, a Git
repository, or an HTTP bundle.

AWS OpsWorks Stacks automatically downloads and deploys applications in built-in layers. For custom layers, you must
include this functionality in your recipe code.

## Users and Permissions Management

AWS OpsWorks Stacks provides the ability to manage users at the stack level, independent of IAM permissions.

## Lifecycle Events

At each layer of a stack, you will set which Chef recipes you would like to execute at each stage of a node’s lifecycle,
such as when it comes online or goes offline. These stages are lifecycle events. The recipes at each lifecycle event
execute in the order you specify in the AWS OpsWorks Agent.

## Chef 11 and Chef 12

Both Chef 11 and Chef 12 provide unique functionality differences that are important to note before you use AWS OpsWorks
Stacks.

## Monitor Instance Metrics

AWS OpsWorks Stacks provides a custom dashboard to monitor up to 13 custom metrics for each instance in the stack. The
agent that runs on each instance will publish the information to the AWS OpsWorks Stacks service.

# Using Amazon Elastic Container Service to Deploy Containers

Amazon ECS is a highly scalable, high-performance container orchestration service that supports Docker containers and
allows you to easily run and scale containerized applications on AWS. Amazon ECS eliminates the need for you to
install and operate your own container orchestration software, manage and scale a cluster of virtual machines, or sched-
ule containers on those virtual machines.

With simple API calls, you can launch and stop Docker-enabled applications, query the complete state of your
application, and access many familiar features such as IAM roles, security groups, load balancers, Amazon CloudWatch
Events, AWS CloudFormation templates, and AWS CloudTrail logs.

## What Is Amazon ECS?

Amazon ECS streamlines the process for managing and scheduling containers across fleets of Amazon EC2 instances, without
the need to include separate management tools for container orchestration or cluster scaling.

AWS Fargate reduces management further as it deploys containers to serverless architecture and removes cluster
management requirements entirely.

To react to changes in demands for your service or application, Amazon ECS supports Amazon EC2 Auto Scaling groups of
cluster instances that allow your service to increase running container counts across multiple instances as demand
increases. You can define container isolation and dependencies as part of the service definition. You can use the
service definition to enforce requirements without user interaction, such as “only one container of type A may run on
a cluster instance at a time.”

## Amazon ECS Concepts

## Amazon ECS Cluster

Amazon ECS clusters are the foundational infrastructure components on which containers run. Clusters consist of one or
more Amazon EC2 instances in your Amazon VPC.

Each instance in a cluster (cluster instance) has an agent installed. The agent is responsible for receiving container
scheduling/shutdown commands from the Amazon ECS service and to report the current health status of containers (restart
or replace).

In an AWS Fargate launch type, Amazon ECS clusters are no longer made up of Amazon EC2 instances. Since the tasks
themselves launch on the AWS infrastructure, AWS assigns each one an elastic network interface with an Amazon VPC.

## AWS Fargate

AWS Fargate simplifies the process of managing containers in your environment and removes the need to manage underlying
cluster instances. Instead, you only need to specify the compute requirements of your containers in your task
definition. AWS Fargate automatically launches containers without your interaction.

AWS Fargate requires that containers launch with the network mode set to awsvpc. In other words, you can launch only AWS
Fargate containers into Amazon VPCs.

## Containers and Images

Any workloads that run on Amazon ECS must reside in Docker containers. In a virtual server environment, multiple virtual
machines share physical hardware, each of which acts as its own operating system.

Container images are similar in concept to AMIs. Images provision a Docker container. You store images in registries,
such as a Docker Hub or an Amazon Elastic Container Repository (ECR).

You can create your own private image repository; however, AWS Fargate does not support this launch type.

## Task Definition

Though you can package entire applications into a single container, it may be more efficient to run multiple smaller
containers, each of which contains a subset of functionality of your full application.

This is referred to as service-oriented architecture (SOA).

A task definition is a JSON document that describes what containers launch for your application or system.

## Services

When creating a service, you can specify the task definition and number of tasks to maintain at any point in time.
After the service creates, it will launch the desired number of tasks; thus, it launches each of the containers in the
task definition. If any containers in the task become unhealthy, the service is responsible and launches replacement
tasks.

## Amazon ECS Service Discovery

Amazon ECS Service Discovery allows you to assign Amazon Route 53 DNS entries automatically for tasks your service
manages. To do so, you create a private service namespace for each Amazon ECS cluster.

A service directory maps DNS entries to available service endpoints. Amazon ECS Service Discovery maintains health
checks of containers, and it removes them from the service directory should they become unavailable.

To use public namespaces, you must purchase or register the public hosted zone with Amazon Route 53.

## Amazon Elastic Container Repository

Amazon Elastic Container Repository (Amazon ECR) is a Docker registry service that is fully compatible with existing
Docker CLI tools. Amazon ECR supports resource-level permissions for private repositories and allows you to preserve a
secure registry without the need to maintain an additional application.

## Amazon ECS Container Agent

The Amazon ECS container agent is responsible for monitoring the status of tasks that run on cluster instances. If a new
task needs to launch, the container agent will download the container images and start or stop containers. If any
containers fail health checks, the container agent will replace them. Since the AWS Fargate launch type uses AWS-managed
compute resources, you do not need to configure the agent.

# Summary

This chapter includes infrastructure, configuration, and deployment services that you use to deploy configuration as
code.

AWS CloudFormation leverages standard AWS APIs to provision and update infrastructure in your account. AWS
CloudFormation uses standard configuration management tools such as Chef and Puppet.

Configuration management of infrastructure over an extended period of time is best served with the use of a dedicated
tool such as AWS OpsWorks Stacks.

You define the configuration in one or more Chef recipes to achieve configuration as code on top of your infrastructure.
AWS OpsWorks Stacks can be used to provide a serverless Chef infrastructure to configure servers with Chef code (
recipes).

Chef recipe code is declarative in nature, and you do not have to rely on the accuracy of procedural steps, as you would
with a userdata script you apply to Amazon ECS instances or launch configurations.

Amazon ECS supports Docker containers, and it allows you to run and scale containerized applications on AWS. Amazon ECS
eliminates the need to install and operate your own container orchestration software, manage and scale a cluster of
virtual machines, or schedule containers on those virtual machines.

AWS Fargate reduces management further as it deploys containers to serverless architecture and removes cluster
management requirements. To create a cluster and deploy services, you configure the resource requirements of containers
and availability requirements. Amazon ECS manages the rest through an agent that runs on cluster instances. AWS
Fargate requires no agent management.

Amazon ECS clusters are the foundational infrastructure components on which containers run. Clusters consist of Amazon
EC2 instances in your Amazon VPC. Each cluster instance has an agent installed that is responsible for receiving
scheduling/shutdown commands from the Amazon ECS service and reporting the current health status of containers (restart
or replace).

AWS OpsWorks Stacks lets you manage applications and servers on AWS and on- premises. You can model your application as
a stack that contains different layers, such as load balancing, database, and application server. You can deploy and
configure Amazon EC2 instances in each layer or connect other resources such as Amazon RDS databases.

AWS OpsWorks Stacks lets you set automatic scaling for your servers on preset schedules or in response to a constant
change of traffic levels, and it uses lifecycle hooks to orchestrate changes as your environment scales. You run Chef
recipes with Chef Solo, which allows you to automate tasks such as installing packages and program languages or
frameworks, configuring software, and more.

An app is the location where you store application code and other files, such as an Amazon S3 bucket, a Git repository,
or an HTTP bundle, and it includes sign-in credentials. The Deploy lifecycle event includes any apps that you
configure for an instance at the layer or layers to which it corresponds.

At each layer of a stack, you set which Chef recipes to execute at each stage of a node’s lifecycle, such as when it
comes online or goes offline (lifecycle events). The recipes at each lifecycle event are executed by the AWS OpsWorks
Agent in the order you specify.

AWS OpsWorks Stacks allows for management of other resources in your account as part of your stack and include elastic
IP addresses, Amazon EBS volumes, and Amazon RDS instances.

The AWS OpsWorks Stacks dashboard monitors up to 13 custom metrics for each instance in the stack. The agent that runs
on each instance will publish the information to the AWS OpsWorks Stacks service. If you enable the layer, system,
application, and custom logs, they automatically publish to Amazon CloudWatch Logs for review without accessing the
instance itself.

When you define a consistent deployment pattern for infrastructure, configuration, and application code, you can convert
entire enterprises to code. You can remove manual management of most common processes and replace them with seamless
management of entire application stacks through a simple commit action.

# Exam Essentials

**Understand configuration management and Chef.**

Configuration management is the process designed to ensure the infrastructure in a given system adheres to a specific
set of standards, settings, or attributes. Chef is a Ruby-based configuration management language that AWS OpsWorks
Stacks uses to enforce configuration on Amazon EC2 on-premises instances, or nodes. Chef uses a declarative syntax to
describe the desired state of a node, abstracting the actual steps needed to achieve the desired configuration. This
code is organized into recipes, which are organized into collections called cookbooks.

**Know how AWS OpsWorks Stacks organizes configuration code into cookbooks.**

In traditional Chef implementations, cookbooks belong to a chef-repo, which is a versioned directory that contains
cookbooks and their underlying recipes and files. A single cookbook repository can contain one or more cookbooks. When
you define the custom cookbook location for a stack, all cookbooks copy to instances in the stack.

**Know how to update custom cookbooks on a node.**

When instances first launch in a stack, they will download cookbooks from the custom cookbook repository. You must
manually issue an Update Custom Cookbooks command to instances in your stack to update the instance.

**Understand the different AWS OpsWorks Stacks components.**

The topmost object in AWS OpsWorks Stacks is a stack, which contains all elements of a given environment or system.
Within a stack, one or more layers contain instances you group by common purpose. A single instance references either
an Amazon EC2 or on-premises instance and contains additional configuration data. A stack can contain one or more
apps, which refer to repositories where application code copies to for deployment. Users are regional resources that you
can configure to access one or more stacks in an account.

**Know the different AWS OpsWorks Stacks instance types and their purpose.**

AWS OpsWorks Stacks has three different instance types: 24/7, time-based, and load-based. The 24/7 instances run
continuously unless an authorized user manually stops it, and they are useful for handling the minimum expected load of
a system. Time-based instances start and stop on a given 24-hour schedule and are recommended for predicable increases
in load at different times of the day. Load-based instances start and stop in response to metrics, such
as CPU utilization for a layer, and you use them to respond to sudden increases in traffic.

**Understand how AWS OpsWorks Stacks implements auto healing.**

The AWS OpsWorks Stacks agent that runs on an instance performs a health check every minute and sends the response to
AWS. If the AWS OpsWorks Stacks agent does not receive the health check for five continuous minutes, the instance
restarts automatically. You can disable this feature. Auto healing events publish to Amazon CloudWatch for reference.

**Understand the AWS OpsWorks Stacks permissions model.**

AWS OpsWorks Stacks provides the ability to manage users at the stack level, independent of IAM permissions. This is
useful for providing access to instances in a stack but not to the AWS Management Console or API. You can assign AWS
OpsWorks Stacks users to one of four permission levels: Deny, Show, Deploy, and Manage. Additionally, you can give users
SSH/RDP access to instances in a stack (with or without sudo/administrator permission). AWS OpsWorks Stacks users are
regional resources. If you would like to give a user in one region access to a stack in another region, you need to copy
the user to the second region. Some AWS OpsWorks Stacks activities are available only through IAM permissions, such as
to delete and create stacks.

**Know the different AWS OpsWorks Stacks lifecycle events.**

Instances in a stack are provisioned, configured, and retired using lifecycle events. The AWS OpsWorks Stacks supports
the lifecycle events: Setup, Configure, Deploy, Undeploy, and Shutdown. The Configure event runs on all instances in a
stack any time one instance comes online or goes offline.

**Know the components of an Amazon ECS cluster.**

A cluster is the foundational infrastructure component on which containers are run. Clusters are made up of one or
more Amazon EC2 instances, or they can be run on AWS-managed infrastructure using AWS Fargate. A task definition is a
JSON file that describes which containers to launch on a cluster. Task definitions can be defined by grouping containers
that are used for a common purpose, such as for compute, networking, and storage requirements. A service launches on a
cluster and specifies the task definition and number of tasks to maintain. If any containers become unhealthy, the
service is responsible for launching replacements.

**Know the difference between Amazon ECS and AWS Fargate launch types.**

The AWS Fargate launch type uses AWS-managed infrastructure to launch tasks. As a customer, you are no longer required
to provision and manage cluster instances. With AWS Fargate, each cluster instance is assigned a network interface in
your VPC. Amazon ECS launch types require a cluster in your account, which you must manage over time.

**Know how to scale running tasks in a cluster.**

Changing the number of instances in a cluster does not automatically cause the number of running tasks to scale in or
out. You can use target tracking policies and step scaling policies to scale tasks automatically based on target
metrics. A target tracking policy determines when to scale based on metrics such as CPU utilization or network traffic.
Target tracking policies keep metrics within a certain boundary. For example, you can launch additional tasks if CPU
utilization is above 75 percent. Step scaling policies can continuously scale as metrics increase or decrease. You can
configure a step scaling policy to scale tasks out when CPU utilization reaches 75 percent and again at 80 percent and
90 percent. A single step scaling policy can result in multiple scaling activities.

**Know how images are stored in Amazon Elastic Container Repository (Amazon ECR).**

Amazon ECR is a Docker registry service that is fully compatible with existing Docker tools. Amazon ECR supports
resource-level permissions for private repositories, and it allows you to maintain a secure registry without the need to
maintain additional instances/ applications.