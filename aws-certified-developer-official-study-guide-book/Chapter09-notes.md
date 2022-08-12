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