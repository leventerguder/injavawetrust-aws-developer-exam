# Optimization

# Introduction to Optimization

Creating a software system is a lot like constructing a building. If the foundation is not solid, structural problems
can undermine the integrity and function of the building.The AWS Well-Architected Tool helps you understand the pros and
cons of decisions that you make while building systems on AWS.

By using the tool, you will learn architectural best practices for designing and operating reliable, secure, efficient,
and cost-effective systems in the AWS Cloud.

When architecting technology solutions, if you neglect the five pillars of operational excellence, security,
reliability, performance efficiency, and cost optimization, it can become challenging to build a system that delivers on
your expectations and requirements. Incorporating these pillars into your architecture helps you to produce stable and
efficient systems.

# Cost Optimization: Everyone’s Responsibility

All teams help manage cloud costs, and cost optimization is everyone’s responsibility. Make sure that costs are known
from beginning to end, at every level, and from executives to engineers. Ensure that project owners and budget holders
know what their upfront and ongoing costs are. Business decision makers must track costs against budgets and understand
return on investment (ROI).

Encourage everyone to track their cost optimization daily so that they can establish a habit of efficiency and see the
daily impact of their cost savings over time.

## Tagging

By tagging your AWS resources, you can assign custom metadata to instances, images, and other resources. For example,
you can categorize resources by owner, purpose, or environment, which helps you organize them and assign cost
accountability. When you apply tags to your AWS resources and activate the tags, AWS adds this information to the Cost
and Usage reports.

### Tag on Creation

You can make tagging a part of your build process and automate it with AWS management tools, such as AWS Elastic
Beanstalk and AWS OpsWorks.

### Enforce Tag Use

Using AWS Identity and Access Management (IAM) policies, you can enforce tag use to gain precise control over access to
resources, ownership, and accurate cost allocation.

# Reduce AWS Usage

Set a continuous practice to review your consumption of AWS resources, and understand the factors that contribute to
cost. Use various AWS monitoring tools to provide visibility, control, and cost optimization.

## Delete Unnecessary EBS Volumes

Stopping an Amazon Elastic Compute Cloud (Amazon EC2) instance leaves any attached Amazon Elastic Block Store (Amazon
EBS) volumes operational. You continue to incur charges for these volumes until you delete them.

## Stop Unused Instances

Stop instances used in development and production during hours when these instances are not in use and then start them
again when their capacity is needed. Assuming a 50-hour workweek, you can save 70 percent of costs by automatically
stopping dev/test/production instances during nonbusiness hours.

## Delete Idle Resources

Consider the following best practices to reduce costs associated with AWS idle resources, such as unattached Amazon EBS
volumes and unused Elastic IP addresses:

- The easiest way to reduce operational costs is to turn off instances that are no longer being used. If you find
  instances that have been idle for more than two weeks, it’s safe to stop or even terminate them.
- Terminating an instance, however, automatically deletes attached EBS volumes and requires effort to re-provision if
  the instance is needed again. If you decide to delete an EBS volume, consider storing a snapshot of the volume so that
  it can be restored later if needed.

## Update Outdated Resources

As AWS releases new services and features, it is a best practice to review your existing architectural decisions to
ensure that they remain cost effective and stay evergreen. As your requirements change, be aggressive in decommissioning
resources, components, and workloads that you no longer require.

## Delete Unused Keys

Each customer master key (CMK) that you create in AWS Key Management Service (AWS KMS), regardless of whether you use it
with KMS-generated key material or key material imported by you, incurs a cost you until you delete it. Before deleting
a CMK, you might want to know how many ciphertexts were encrypted under that key. Knowing how a CMK was used in the past
might help you decide whether you will need it in the future by using AWS CloudTrail usage logs. After you are sure that
you want to delete a CMK in AWS KMS, schedule the key deletion.

## Delete Old Snapshots

If your architecture suggests a backup policy that takes EBS volume snapshots daily or weekly, then you will quickly
accumulate snapshots. To reduce storage costs, check for “stale” snapshots—ones that are more than 30 days old—and
delete them. Deleting a snapshot has no effect on the volume. You can use the AWS Management Console or AWS Command Line
Interface (AWS CLI) for this purpose.

# Right Sizing

Right sizing is the process of matching instance types and sizes to performance and capac- ity requirements at the
lowest possible cost. To achieve cost optimization, right sizing must become an ongoing process within your
organization. Even if you right size workloads initially, performance and capacity requirements can change over time,
which can result in underused or idle resources.

## Select the Right Use Case

As you monitor current performance, identify the following usage needs and patterns so that you can take advantage of
potential right-sizing options:

**Steady State**

The load remains constant over time, making forecasting simple. Consider using Reserved Instances to gain significant
savings.

**Variable, but predictable**

The load changes on a predictable schedule. Consider using AWS Auto Scaling.

**Dev, test, production**

Development, testing, and production environments can usually be turned off outside of work hours.

**Temporary**

Temporary workloads that have flexible start times and can be interrupted are good candidates for Spot Instances instead
of On-Demand Instances.

## Select the Right Instance Family

When you launch an instance, the instance type that you specify determines the hardware of the host computer used for
your instance. Each instance type offers different compute, memory, and storage capabilities, and they are grouped in
instance families based on these capabilities. Depending on the AWS offering, you can determine the right instance
family for your infrastructure.

### Amazon Elastic Cloud Compute

Following are the different options for CPU, memory, and network resources:

- General purpose (includes A1, T2, M3, and M4 instance types)
- Compute optimized (includes the C3 and C4 instance types)
- Memory optimized (includes the X1, R3, and R4 instance types)
- Storage optimized (includes the I3 and D2 instance types)
- Accelerated computing (includes the P2, G3, and F1 instance types)

### Amazon Relational Database Service

- Standard performance (includes the M3 and M4 instance types)
- Burstable performance (includes T2 instance types)
- Memory optimized (includes the R3 and R4 instance types)

## Select the Right Instance Compatibility

- Virtualization type
- Network
- Platform

# Using Instance Reservations

## AWS Pricing for Reserved Instances

Amazon EC2 Reserved Instances allow you to commit to usage parameters. To unlock an hourly rate that is up to 75 percent
lower than On-Demand pricing, you can commit to a one-year or three-year duration at the time of purchase.

There are three payment options for Reserved Instances:

- No Upfront
- Partial Upfront
- All Upfront

## Amazon EC2 Reservations

Amazon EC2 Reserved Instances provide a reservation of resources and capacity when used in a specific Availability Zone
within an AWS Region:

- With Reserved Instances, you commit to a period of usage (one or three years) and save up to 75 percent over
  equivalent On-Demand hourly rates.
- For applications that have steady state or predictable usage, Reserved Instances can provide significant savings
  compared to using On-Demand Instances, without requiring a change to your workload.

### Convertible Reserved Instances

Convertible Reserved Instances are provided for a one-year or three-year term, and they enable conversion to different
families, new pricing, different instance sizes, different platforms, or tenancy during the period.

Use Convertible Reserved Instances when you are uncertain about instance needs in the future, but you are still
committed to using Amazon EC2 instances for a three-year term in exchange for a significant discount.

### Reserved Instance Marketplace

Use the Reserved Instance Marketplace to sell your unused Reserved Instances and buy Reserved Instances from other AWS
customers.

# Amazon Relational Database Service Reservations

Reserved DB instances are not physical instances; they are a billing discount applied to the use of certain on-demand DB
instances in your account. Discounts for reserved DB instances are tied to instance type and AWS Region.

All Reserved Instance types are available for Amazon Aurora, MySQL, MariaDB, PostgreSQL, Oracle, and SQL Server database
engines.

Reserved Instances can also provide significant cost savings for mission-critical applications that run on Multi-AZ
database deployments for higher availability and data durability. Reserved Instances can minimize your costs up to 69
percent over On-Demand rates when used in steady state.

The Reserved Instance discounted rate also applies to usage of both Single-AZ and Multi-AZ configurations for the same
database engine and instance family.

# Using Spot Instances

Amazon EC2 Spot Instances offer spare compute capacity in the AWS Cloud at steep dis- counts compared to On-Demand
Instances.

You can use Spot Instances to save up to 90 percent on stateless web applications, big data, containers, continuous
integration/continuous delivery (CI/CD), high performance computing (HPC), and other fault-tolerant workloads. Or, scale
your workload throughput by up to 10 times and stay within the existing budget

## Spot Fleets

Use Spot Fleets to request and manage multiple Spot Instances automatically, which provides the lowest price per unit
of capacity for your cluster or application, such as a batch-processing job, a Hadoop workflow, or an HPC grid
computing job. You can include the instance types that your application can use. You define a target capacity based on
your application needs (in units, including instances, vCPUs, memory, storage, or network throughput) and update the
target capacity after the fleet is launched. Spot Fleets enable you to launch and maintain the target capacity and to
request resources automatically to replace any that are disrupted or manually terminated.

## Amazon EC2 Fleets

With a single API call, Amazon EC2 Fleet enables you to provision compute capacity across different instance types,
Availability Zones, and across On-Demand, Reserved Instances, and Spot Instances purchase models to help optimize scale,
performance, and cost.

## Design for Continuity

With Spot Instances, you avoid paying more than the maximum price you specified. If the Spot price exceeds your maximum
willingness to pay for a given instance or when capacity is no longer available, your instance is terminated
automatically (or stopped or hibernated, if you opt for this behavior on a persistent request).

# Using AWS Auto Scaling

Using AWS Auto Scaling, you can scale workloads in your architecture. It automatically increases the number of resources
during the demand spikes to maintain performance and decreases capacity when demand lulls to reduce cost.

## Amazon EC2 Auto Scaling

Amazon EC2 Auto Scaling helps you scale your Amazon EC2 instances and Spot Fleet capacity up or down automatically
according to conditions that you define.

AWS Auto Scaling is generally used with Elastic Load Balancing to distribute incoming application traffic across
multiple Amazon EC2 instances in an AWS Auto Scaling group. AWS Auto Scaling is triggered using scaling plans that
include policies that define how to scale (manual, schedule, and demand spikes) and the metrics and alarms to monitor in
Amazon CloudWatch.

You can use Amazon EC2 Auto Scaling to increase the number of Amazon EC2 instances automatically during demand spikes to
maintain performance and decrease capacity during lulls to reduce costs.

### Dynamic Scaling

The dynamic scaling capabilities of Amazon EC2 Auto Scaling refers to the functionality that automatically increases
or decreases capacity based on load or other metrics.

### Scheduled Scaling

Scaling based on a schedule allows you to scale your application ahead of known load changes, such as the start of
business hours, thus ensuring that resources are available when users arrive, or in typical development or test
environments that run only during defined business hours or periods of time.

### Fleet Management

Fleet management refers to the functionality that automatically replaces unhealthy instances in your application,
maintains your fleet at the desired capacity, and balances instances across Availability Zones. Amazon EC2 Auto Scaling
fleet management ensures that your application is able to receive traffic and that the instances themselves are
working properly. When AWS Auto Scaling detects a failed health check, it can replace the instance automatically.

### Instances Purchasing Options

With Amazon EC2 Auto Scaling, you can provision and automatically scale instances across purchase options, Availability
Zones, and instance families in a single application to optimize scale, performance, and cost. You can include Spot
Instances with On-Demand and Reserved Instances in a single AWS Auto Scaling group to save up to 90 percent on compute.

### Golden Images

A golden image is a snapshot of a particular state of a resource, such as an Amazon EC2 instance, Amazon EBS volumes,
and an Amazon RDS DB instance. You can customize an Amazon EC2 instance and then save its configuration by creating an
Amazon Machine Image (AMI)

## AWS Auto Scaling

AWS Auto Scaling monitors your applications and automatically adjusts capacity of all scalable resources to maintain
steady, predictable performance at the lowest possible cost. Using AWS Auto Scaling, you can set up application scaling
for multiple resources across multiple services in minutes.

AWS Auto Scaling automatically scales resources for other AWS services, including Amazon ECS, Amazon DynamoDB, Amazon
Aurora, Amazon EC2 Spot Fleet requests, and Amazon EC2 Scaling groups.

The predictive scaling feature uses machine learning algorithms to detect changes in daily and weekly patterns,
automatically adjusting their forecasts. This removes the need for the manual adjustment of AWS Auto Scaling parameters
as cyclicality changes over time, making AWS Auto Scaling simpler to configure, and provides more accurate capacity
provisioning. Predictive scaling results in lower cost and more responsive applications.

## DynamoDB Auto Scaling

DynamoDB automatic scaling uses the AWS Auto Scaling service to adjust provisioned throughput capacity dynamically on
your behalf in response to actual traffic patterns. This enables a table or a global secondary index to increase its
provisioned read and write capacity to handle sudden increases in traffic without throttling. When the workload
decreases, AWS Auto Scaling decreases the throughput so that you don’t pay for unused provisioned capacity.

## Amazon Aurora Auto Scaling

Amazon Aurora automatic scaling dynamically adjusts the number of Aurora Replicas provisioned for an Aurora DB
cluster. Aurora automatic scaling is available for both Aurora MySQL and Aurora PostgreSQL.

Amazon Aurora Serverless is an on-demand, automatic scaling configuration for the MySQL-compatible edition of Amazon
Aurora.

# Using Containers

Containers provide a standard way to package your application’s code, configurations, and dependencies into a single
object. Containers share an operating system installed on the server and run as resource-isolated processes, ensuring
quick, reliable, and consistent deployments, regardless of environment.

## Containerize Everything

Use Amazon Elastic Container Service (Amazon ECS) to build all types of containerized applications easily, from
long-running applications and microservices to batch jobs and machine learning applications. You can migrate legacy
Linux or Windows applications from on-premises to the AWS Cloud and run them as containerized applications using Amazon
ECS.

Amazon ECS maintains application availability and allows you to scale your containers up or down to meet your
application’s capacity requirements.

Amazon ECS is integrated with familiar features like Elastic Load Balancing, EBS volumes, virtual private cloud (VPC),
and AWS Identity and Access Management (IAM). Use APIs to integrate and use your own schedulers or connect Amazon ECS
into your existing software delivery process.

## Containers without Servers

AWS Fargate technology is available with Amazon ECS. With Fargate, you no longer have to select Amazon EC2 instance
types, provision and scale clusters, or patch and update each server. You do not have to worry about task placement
strategies, such as binpacking or host spread, and tasks are automatically balanced across Availability Zones. Fargate
manages the availability of containers for you.
