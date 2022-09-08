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

# Using Serverless Approaches

Serverless approaches are ideal for applications whereby load can vary dynamically. Using a serverless approach means no
compute costs are incurred when there is no user traffic, while still offering instant scale to meet high demand, such
as a flash sale on an ecommerce site or a social media mention that drives a sudden wave of traffic. All of the actual
hardware and server software are handled by AWS.

Benefits gained by using AWS Serverless services include the following:

- No need to manage servers
- No need to ensure application fault tolerance, availability, and explicit fleet management to scale to peak load
- No charge for idle capacity

You can focus on product innovation and rapidly construct these applications:

- Amazon S3 offers a simple hosting solution for static content.
- AWS Lambda, with Amazon API Gateway, supports dynamic API requests using functions.
- Amazon DynamoDB offers a simple storage solution for session and per-user state.
- Amazon Cognito provides a way to handle user registration, authentication, and access control to resources.
- AWS Serverless Application Model (AWS SAM) can be used by developers to describe the various elements of an
  application.
- AWS CodeStar can set up a CI/CD toolchain with a few clicks.

## Optimize Lambda Usage

AWS Lambda provides the cloud-logic layer, and with Lambda you can run code for virtually any type of application or
backend service, all with zero administration.

A variety of events can trigger Lambda functions, enabling developers to build reactive, event-driven systems without
managing infrastructure.

Consider the following recommendations for optimizing Lambda functions:

**Optimal memory size**

The memory usage for your function is determined per invocation and can be viewed in CloudWatch Logs. By analyzing the
Max Memory Used: field in the Invocation report, you can determine whether your function needs more memory or whether
you over-provisioned your function’s memory size.

**Language runtime performance**

If your application use case is both latency-sensitive and susceptible to incurring the initial invocation cost
frequently (spiky traffic or infrequent use), then recommend one of the interpreted languages, such as Node.js or
Python.

**Optimizing code**

Much of the application performance depends on your logic and dependencies. Pay attention to reusing the objects and
using global/static variables. Keep live or reuse HTTP/session connections, and use default network environments as much
as possible.

# Optimizing Storage

AWS storage services are optimized for different storage scenarios—there is no single data storage option that is ideal
for all workloads. When evaluating your storage requirements, consider data storage options for each workload
separately.

Amazon offers three broad categories of storage services: object, block, and file storage.

## Object Storage

Amazon Simple Storage Service (Amazon S3) is highly durable, general-purpose object storage that works well for
unstructured datasets such as media content.

There are multiple tiers of storage: hot, warm, or cold data. In terms of pricing, the colder the data, the cheaper it
is to store, and the costlier it is to access when needed.

**Standard (STANDARD)**

This is the best storage option for data that you frequently access. Amazon S3 delivers low latency and high throughput,
and it is ideal for use cases such as cloud applications, dynamic websites, content distribution, gaming, and data
analytics.

**Amazon S3 Standard – Infrequent Access (STANDARD_IA)**

Use this storage option for data that you access less frequently, such as long-term backups and disaster recovery. It
offers cheaper storage over time, but higher charges to retrieve or transfer data.

**Amazon S3 Intelligent-Tiering (INTELLIGENT_TIERING)**

This storage class is designed to optimize the cost by moving data to the most cost-effective access tier automatically
without degrading the performance of the application. If an object in the infrequent access tier is accessed, it is
automatically moved back to the frequent access tier.

**Amazon S3 One Zone-Infrequent Access (ONEZONE_IA)**

This storage class provides a lower-cost option for infrequently accessed data that requires rapid access. The data is
stored in only one Availability Zone (AZ), and it saves up to 20 percent of storage costs as compared to STANDARD_IA.
Use this option for storing secondary backups of on-premises data or data that can be easily recreated.

**Amazon S3 Glacier (GLACIER)**

This option is designed for long-term storage of infrequently accessed data, such as end-of-lifecycle, compliance, or
regulatory backups. Different methods of data retrieval are available at various speeds and cost. Retrieval can take
from a few minutes to several hours.

**Amazon S3 Glacier Deep Archive (DEEP_ARCHIVE)**

This is the lowest-cost class designed for long-term retention of rarely accessed data. Data will be retained for 7–10
years and may be accessed about once or twice a year. When you need the data, you can retrieve it within 12 hours. This
storage is ideal for maintaining backups of historical regulatory or compliance data and disaster recovery backups.

## Block Storage

Amazon Elastic Block Store (Amazon EBS) volumes provide a durable block-storage option for use with Amazon EC2
instances.

There are two types of block storage: solid-state drive (SSD) storage and hard disk drive (HDD) storage.

SSD storage is optimized for transactional workloads wherein performance is closely tied to IOPS. Choose from two SSD
volume options:

**General Purpose SSD (gp2)**

Designed for general use and offers a balance between cost and performance.

**Provisioned IOPS SSD (io1)**

Best for latency-sensitive workloads that require specific minimum-guaranteed IOPS. With io1 volumes, you pay separately
for Provisioned IOPS, so unless you need high levels of Provisioned IOPS, gp2 volumes are a better match at lower cost.

HDD storage is designed for throughput-intensive workloads, such as data warehouses and log processing. There are two
types of HDD volumes:

**Throughput Optimized HDD (st1)**

Best for frequently accessed, throughput-intensive workloads.

**Cold HDD (sc1**

Designed for less frequently accessed, throughput-intensive workloads.

## File Storage

Amazon Elastic File System (Amazon EFS) provides simple, scalable file storage for use with Amazon EC2 instances. Amazon
EFS supports any number of instances at the same time. Amazon EFS is designed for workloads and applications such as big
data, media-processing workflows, content management, and web serving.

## Optimize Amazon S3

policies. Identifying the right storage class and moving less frequently accessed Amazon S3 data to cheaper storage
tiers yields considerable savings. For example, by moving data from the STANDARD to STANDARD_IA storage class, you can
save up to 60 percent (on a per-gigabyte basis) of Amazon S3 pricing. By moving data that is at the end of its lifecycle
and accessed on rare occasions from Amazon S3 Glacier, you can save up to 80 percent of Amazon S3 pricing.

## Storage Management Tools/Features

### Cost Allocation S3 Bucket Tags

To track the storage cost or other criteria for individual projects or groups of projects, label your Amazon S3 buckets
using cost allocation tags. A cost allocation tag is a key-value pair that you associate with an S3 bucket. To manage
storage data most effectively, you can use these tags to categorize your S3 objects and filter on these tags in your
data lifecycle policies.

### Amazon S3 Analytics: Storage Class Analysis

Use this feature to analyze storage access patterns to help you decide when to transition the right data to the right
storage class. This feature observes data access patterns to help you determine when to transition less frequently
accessed STANDARD storage to the STANDARD_IA storage class.

### Amazon S3 Inventory

This tool audits and reports on the replication and encryption status of your S3 objects
on a weekly or monthly basis. This feature provides CSV output files that list objects and their corresponding metadata,
and it lets you configure multiple inventory lists for a single bucket, organized by different Amazon S3 metadata tags.
You can also query Amazon S3 inventory through standard SQL by using Amazon Athena, Amazon Redshift Spectrum, and other
tools, such as Presto, Apache Hive, and Apace Spark.

### Amazon CloudWatch

Amazon S3 can also publish storage, request, and data transfer metrics to Amazon CloudWatch.

### Use Amazon S3 Select

Amazon S3 Select enables applications to retrieve only a subset of data from an object by using simple SQL expressions.

### Use Amazon Glacier Select

Amazon Glacier Select unlocks an opportunity to query your archived data easily. With Glacier Select, you can filter
directly against an Amazon S3 Glacier object by using stan- dard SQL statements.

## Optimize Amazon EBS

With Amazon EBS, you are paying for provisioned capacity and performance—even if the volume is unattached or has low
write activity. To optimize storage performance and costs for Amazon EBS, monitor volumes periodically to identify ones
that are unattached or appear to be underutilized or overutilized, and adjust provisioning to match actual usage.

## Use Monitoring Tools

AWS offers tools that help you optimize block storage.

### Amazon CloudWatch

Amazon CloudWatch automatically collects a range of data points for EBS volumes, and you can then set alarms on volume
behavior.

### AWS Trusted Advisor

AWS Trusted Advisor is another way for you to analyze your infrastructure to identify unattached, underutilized, and
overutilized EBS volumes.

## Delete Unattached Amazon EBS Volumes

To find unattached EBS volumes, look for volumes that are available, which indicates that they are not attached to an
Amazon EC2 instance. You can also look at network throughput and IOPS to determine whether there has been any volume
activity over the previous two weeks, or you can look up the last time the EBS volume was attached. If the volume is in
a nonproduction environment, hasn’t been used in weeks, or hasn’t been attached in a month, there is a good chance that
you can delete it.

## Resize or Change the EBS Volume Type

- For General Purpose SSD gp2 volumes, optimize for capacity so that you’re paying only for what you use.
- With Provisioned IOPS SSD io1 volumes, pay close attention to IOPS utilization rather than throughput, since you pay
  for IOPS directly. Provision 10–20 percent above maximum IOPS utilization.
- You can save by reducing Provisioned IOPS or by switching from a Provisioned IOPS SSD io1 volume type to a General
  Purpose SSD gp2 volume type
- If the volume is 500 GB or larger, consider converting to a Cold HDD sc1 volume to save on your storage rate.

## Delete Stale Amazon EBS Snapshots

If you have a backup policy that takes EBS volume snapshots daily or weekly, you will quickly accumulate snapshots.
Check for stale snapshots that are more than 30 days old and delete them to reduce storage costs. Deleting a snapshot
has no effect on the volume.

# Optimizing Data Transfer

Optimizing data transfer ensures that you minimize data transfer costs. Review your user presence if global or local and
how the data gets located in order to reduce the latency issues.

- Use Amazon CloudFront, a global content delivery network (CDN), to locate data closer to users. It caches data at edge
  locations across the world, which reduces the load on your resources. By using CloudFront, you can reduce the
  administrative effort in delivering content automatically to large numbers of users globally, with minimum latency.
  Depending on your application types, distribute your entire website, including dynamic, static, streaming, and
  interactive content through CloudFront instead of scaling out your infrastructure.
- Amazon S3 transfer acceleration enables fast transfer of files over long distances between your client and your S3
  bucket. Transfer acceleration leverages Amazon CloudFront globally distributed edge locations to route data over an
  optimized network path. For a workload in an S3 bucket that has intensive GET requests, you should use Amazon S3 with
  CloudFront.
- When uploading large files, use multipart uploads with multiple parts uploading at once to help maximize network
  throughput. Multipart uploads provide the following advantages:
    - Improved throughput—You can upload parts in parallel to improve throughput.
    - Quick recovery from any network issues—Smaller part size minimizes the impact of restarting a failed upload due to
      a network error.
    - Pause and resume object uploads—You can upload object parts over time. After you initiate a multipart upload,
      there is no expiry; you must explicitly complete or abort the multipart upload.
    - Begin an upload before you know the final object size—You can upload an object as you are creating it.
- Using Amazon Route 53, you can reduce latency for your users by serving their requests from the AWS Region for which
  network latency is lowest. Amazon Route 53 latency-based routing lets you use Domain Name System (DNS) to route user
  requests to the AWS Region that will give your users the fastest response.

## Caching

Caching improves application performance by storing frequently accessed data items in memory so that they can be
retrieved without accessing the primary data store. Cached information might include the results of I/O-intensive
database queries or the outcome of computationally intensive processing.

## Amazon ElastiCache

Amazon ElastiCache is a web service that makes it easy to deploy, operate, and scale an in-memory cache in the cloud. It
supports two open-source, in-memory caching engines: Memcached and Redis.

- The Memcached caching engine is popular for database query results caching, session caching, webpage caching, API
  caching, and caching of objects such as images, files, and metadata. Memcached is also a great choice to store and
  manage session data for internet-scale applications in cases wherein persistence is not critical.
- Redis caching engine is a great choice for implementing a highly available in-memory cache to decrease data access
  latency, increase throughput, and ease the load off your relational or NoSQL database and application. Redis has disk
  persistence built in, and you can use it for long-lived data.

Lazy loading is a good caching strategy whereby you populate the cache only when an object is requested by the
application, keeping the cache size manageable. Apply a lazy caching strategy anywhere in your application where you
have data that is going to be read often but written infrequently. In a typical web or mobile app, for example, a user’s
profile rarely changes but is accessed throughout the application.

## Amazon DynamoDB Accelerator (DAX)

Amazon DynamoDB Accelerator (DAX) is a fully managed, highly available, in-memory cache for Amazon DynamoDB. This
feature delivers performance improvements from milliseconds to microseconds, for high throughput. DAX adds in-memory
acceleration to your DynamoDB tables without requiring you to manage cache invalidation, data population, or clusters.

DAX is ideal for applications that require the fastest possible response time read opera- tions but that are also
cost-sensitive and require repeated reads against a large set of data. For example, consider an ecommerce system that
has a one-day sale on a popular product that would sharply increase the demand or a long-running analysis of regional
weather data that could temporarily consume all of the read capacity in a DynamoDB table.

# Relational Databases and Amazon DynamoDB

Traditional relational database management system (RDBMS) platforms store data in a normalized relational structure that
reduces hierarchical data structures to a set of common elements that are stored across multiple tables.

A relational database system does not scale well for the following reasons:

- It normalizes data and stores it on multiple tables that require multiple queries to write to disk.
- It generally incurs the performance costs of an Atomicity, Consistency, Isolation, Durability (ACID)–compliant
  transaction system.
- It uses expensive joins to reassemble required views of query results.

For this reason, when your business requires a low-latency response to high-traffic que- ries, taking advantage of a
NoSQL system generally makes technical and economic sense. Amazon DynamoDB helps solve the problems that limit
relational system scalability by avoiding them.

DynamoDB scales well for these reasons:

- Schema flexibility lets Amazon DynamoDB store complex hierarchical data within a single item.
- Composite key design lets it store related items close together on the same table.

## Apply NoSQL Design

NoSQL design requires a different mind-set than RDBMS design. For an RDBMS, you can create a normalized data model
without thinking about access patterns. You can then extend it later when new questions and query requirements arise.

NoSQL design is different:

- For DynamoDB, by contrast, design your schema after you know the questions it needs to answer. Understanding the
  business problems and the application use cases up front is essential.
- Maintain as few tables as possible in an Amazon DynamoDB application. Most well- designed applications require only
  one table.

## Keep Related Data Together

Keeping related data in proximity has a major impact on cost and performance. Instead of distributing related data items
across multiple tables, keep related items in your NoSQL system as close together as possible.

## Keep Fewer Tables

In general, maintain as few tables as possible in an Amazon DynamoDB application. Most well-designed applications
require only one table, unless there is a specific reason for using multiple tables.

## Distribute Workloads Evenly

The optimal usage of a table’s provisioned throughput depends on the workload patterns of individual items and the
partition key design.

### Designing Partition Keys

![](Samples of Partition Key Distributions.png)

### Keep the Number of Indexes to a Minimum

Create secondary indexes on attributes that are queried often. Indexes that are seldom used contribute to increased
storage and I/O costs without improving application performance.

### Choose Projections Carefully

Because secondary indexes consume storage and provisioned throughput, keep the size
of the index as small as possible. Also, the smaller the index, the greater the performance advantage compared to
querying the full table. Project only the attributes that you regularly request. Every time you update an attribute that
is projected in an index, you incur the extra cost of updating the index as well.

### Use Sparse Indexes

For any item in a table, Amazon DynamoDB writes a corresponding index entry only if the index sort key value is present
in the item. If the sort key doesn’t appear in every table item, the index is said to be sparse.

### Avoid Scans as Much as Possible

In general, Scan operations are less efficient than other operations in DynamoDB. A Scan operation scans the entire
table or secondary index. It then filters out values to provide the result you want.

If possible, avoid using a Scan operation on a large table or index with a filter that removes many results. Also, as a
table or index grows, the Scan operation slows down.

# Monitoring Costs

## Cost Management Tools

AWS provides tools to help you identify those cost-saving opportunities and keep your resources right-sized. Use these
tools to help you access, organize, understand, control, and optimize your costs.

## AWS Trusted Advisor

AWS Trusted Advisor is an online tool that provides you with real-time guidance to help you provision your resources
following AWS best practices.

Whether you’re establishing new workflows or developing applications, or as part of ongoing improvements, take advantage
of the recommendations provided by Trusted Advisor on a regular basis. By reviewing the recommendations, you can look
for opportunities to save money.

Here are some Trusted Advisor checks that help you determine how to reduce your bill:

- Low utilization of Amazon EC2 instances
- Idle resources, such as load balancers and Amazon RDS DB instances
- Underutilized Amazon EBS volumes and Amazon Redshift clusters
- Unassociated Elastic IP addresses
- Optimization, lease expiration—Amazon Reserved Instances
- Inefficiently configured Amazon Route 53 latency record sets

## AWS Cost Explorer

Use the AWS Cost Explorer tool to dive deeper into your cost and usage data to identify trends, pinpoint cost drivers,
and detect anomalies. It includes Amazon EC2 usage reports, which let you analyze the cost and usage of your Amazon EC2
instances over the last 13 months.

**Monthly Costs by AWS Service**

Allows you to visualize the costs and usage associated with your top five cost-accruing AWS services and gives you a
detailed breakdown on all services in the table view. The reports let you adjust the time range to view historical data
going back up to 12 months to gain an understanding of your cost trends.

**Amazon EC2 Monthly Cost and Usage**

Lets you view all AWS costs over the past two months, in addition to your current month-to-date costs. From there, you
can drill down into the costs and usage associated with particular linked accounts, regions, tags, and more.

**Monthly Costs by Linked Account**

Allows you to view the distribution of costs across your organization.

**Monthly Running Costs**

Provides an overview of all running costs over the past three months and provides forecasted numbers for the coming
month with a corresponding confidence interval. This report gives you good insight into how your costs are trending
and helps you plan ahead.

## AWS Cost Explorer API

Use AWS Cost Explorer API to query your cost and usage data programmatically (using AWS CLI or AWS SDKs). You can query
for aggregated data such as total monthly costs or total daily usage. You can also query for granular data, such as the
number of daily write operations for Amazon DynamoDB database tables in your production environment.

You can access your Amazon EC2 Reserved Instance purchase recommendations programmatically through the AWS Cost
Explorer API. Recommendations for Reserved Instance purchases are calculated based on your past usage and indicate
opportunities for potential cost savings.

## AWS Budgets

With AWS Budgets, you can set custom budgets that alert you when your costs or usage exceed (or are forecasted to
exceed) your budgeted amount. You can also use AWS Budgets to set Reserved Instance utilization or coverage targets and
receive alerts when your utilization drops below the threshold you define. Reserved Instance alerts support Amazon
EC2, Amazon RDS, Amazon Redshift, and Amazon ElastiCache reservations.

Budgets can be tracked at the monthly, quarterly, or yearly level, and you can customize the start and end dates. You
can further refine your budget to track costs associated with multiple dimensions, such as AWS service, linked account,
tag, and others. You can send budget alerts through email or Amazon Simple Notification Service (Amazon SNS) topic.

## AWS Cost and Usage Report

The AWS Cost and Usage Report tracks your AWS usage and provides estimated charges associated with that usage. You can
configure this report to present the data hourly or daily. It is updated at least once a day until it is finalized at
the end of the billing period. The AWS Cost and Usage report gives you the most granular insight possible into your
costs and usage, and it is the source of truth for the billing pipeline. It can be used to develop advanced custom
metrics using business intelligence, data analytics, and third-party cost optimization tools.

## Amazon CloudWatch

Amazon CloudWatch is a monitoring service for AWS Cloud resources and the applications you run on AWS. You can use
Amazon CloudWatch to collect and track metrics and log files, set alarms, and automatically react to changes in your AWS
resources. You can create an alarm to perform one or more of the following actions based on the value of the metric:

- Automatically stop or terminate Amazon EC2 instances that have gone unused or underutilized for too long
- Stop your instance if it has an EBS volume as its root device

Amazon CloudWatch Events deliver a near real-time stream of system events that describe changes in AWS resources. Using
simple rules, you can route each type of event to one or more targets, such as Lambda functions, Amazon Kinesis streams,
and Amazon SNS topics.

## AWS Cost Optimization Monitor

AWS Cost Optimization Monitor is an automated reference deployment solution that processes detailed billing reports to
provide granular metrics that you can search, analyze, and visualize in a customizable dashboard. The solution uploads
detailed billing report data automatically to Amazon Elasticsearch Service (Amazon ES) for analysis and leverages its
built-in support for Kibana, enabling you to visualize the first batch of data as soon as it’s processed.

## Cost Optimization: Amazon EC2 Right Sizing

Amazon EC2 Right Sizing is an automated AWS reference deployment solution that uses managed services to perform a
right-sizing analysis and offer detailed recommendations for more cost-effective instances. The solution analyzes two
weeks of utilization data to provide detailed recommendations for right sizing your Amazon EC2 instances.

# Monitoring Performance

After you have implemented your architecture, monitor its performance so that you can remediate any issues before your
customers are aware of them. Use monitoring metrics to raise alarms when thresholds are breached. The alarm can trigger
automated action to work around any components with poor performance.
AWS provides tools that you can use to monitor the performance, reliability, and availability of your resources on the
AWS Cloud.

## Amazon CloudWatch

Amazon CloudWatch is essential to performance efficiency, which provides system-wide visibility into resource
utilization, application performance, and operational health.

You can create an alarm to monitor any Amazon CloudWatch metric in your account. For example, you can create alarms on
an Amazon EC2 instance CPU utilization, Elastic Load Balancing request latency, Amazon DynamoDB table throughput, or
Amazon SQS queue length.

## AWS Trusted Advisor

AWS Trusted Advisor inspects your AWS environment and makes recommendations that help to improve the speed and
responsiveness of your applications.

The following are a few Trusted Advisor checks to improve the performance of your service. The Trusted Advisor checks
your service limits, ensuring that you take advantage of provisioned throughput, and monitors for overutilized
instances:

- Amazon EC2 instances that are consistently at high utilization can indicate optimized, steady performance, but this
  check can also indicate that an application does not have enough resources.
- Provisioned IOPS (SSD) volumes that are attached to an Amazon EC2 instance that is not Amazon EBS–optimized. Amazon
  EBS volumes are designed to deliver the expected performance only when they are attached to an EBS-optimized instance.
- Amazon EC2 security groups with a large number of rules.
- Amazon EC2 instances that have a large number of security group rules.
- Amazon EBS magnetic volumes (standard) that are potentially overutilized and might benefit from a more efficient
  configuration.
- CloudFront distributions for alternate domain names with incorrectly configured DNS settings.

# Summary

In this chapter, you learned about the following:

- Cost-optimizing practices
- Right sizing your infrastructure
- Optimizing using Reserved Instances, Spot Instances, and AWS Auto Scaling
- Optimizing storage and data transfer
- Optimizing using NoSQL database (Amazon DynamoDB)
- Monitoring your costs and performance
- Tools, such as AWS Trusted Advisor, Amazon CloudWatch, and AWS Budgets

Achieving an optimized system is a continual process. An optimized system uses all
the provisioned resources efficiently and achieves your business goal at the lowest price point. Engineers must know the
cost of deploying resources and how to architect for cost optimization. Practice eliminating the waste and bring
accountability in every step of the build process.

Define IAM policies to enforce tag usage, and use tagging tools, such as AWS Config and AWS Tag Editor, to manage tags.
Be cost-conscious, reduce the usage by terminating unused instances, and delete old snapshots and unused keys.

Right size your infrastructure by matching instance types and sizes, and set periodic checks to ensure that the initial
provision remains optimum as your business changes over time. With Amazon EC2, you can choose the combination of
instance types and sizes most appropriate for your applications. Amazon RDS instances are also optimized for memory,
performance, and I/O.

Amazon EC2 Reserved Instances provide you with a significant discount (up to 75 percent) compared to On-Demand Instance
pricing. Using Convertible Reserved Instances, you can change instance families, OS types, and tenancies while
benefitting from Reserved Instance pricing. Reserved Instance Marketplace allows you to sell the unused Reserved
Instances or buy them from other AWS customers, usually at lower prices and shorter terms. With size flexibility,
discounted rates for Amazon RDS Reserved Instances are automatically applied to the usage of any size within the
instance family.

Spot Instances provide an additional option for obtaining compute capacity at a reduced cost and can be used along with
On-Demand and Reserved Instances. Spot Fleets enable you to launch and maintain the target capacity and to request
resources automatically to replace any that are disrupted or manually terminated. Using the termination notices and
persistent requests in your application design help to maintain continuity as the result of interruptions.

AWS Auto Scaling automatically scales if your application experiences variable load and uses one or more scalable
resources, such as Amazon ECS, Amazon DynamoDB, Amazon Aurora, Amazon EC2 Spot requests, and Amazon EC2 scaling groups.
Predictive Scaling uses machine learning models to forecast daily and weekly patterns. Amazon EC2 Auto Scaling enables
you to scale in response to demand and known load schedules. It supports the provisioning of scale instances across
purchase options, Availability Zones, and instance families to optimize performance and cost.

Containers provide process isolation and improve the resource utilization. Amazon ECS lets you easily build all types of
containerized applications and launch thousands of containers in seconds with no additional complexity. With AWS
Fargate technology, you can manage containers without having to provision or manage servers. It enables you to focus on
building and running applications, not the underlying infrastructure.

AWS Lambda takes care of receiving events or client invocations and then instantiates and runs the code. That means
there’s no need to manage servers. Serverless services have built-in automatic scaling, availability, and fault
tolerance. These features allow you to focus on product innovation and rapidly construct applications, such as web
applications, websites, web-hooked systems, chatbots, and clickstream.

AWS storage services are optimized to meet different storage requirements. Use the Amazon S3 analytics feature to
analyze storage access patterns to help you decide when to transition the right data to the right storage class and to
yield considerable savings. Monitor Amazon EBS volumes periodically to identify ones that are unattached or appear to be
underutilized or overutilized, and adjust provisioning to match actual usage.

Optimizing data transfer ensures that you minimize data transfer costs. Use options such as Amazon CloudFront, Amazon S3
transfer acceleration, and Amazon Route 53 to let data reach Regions faster and reduce latency issues.

NoSQL database systems like Amazon DynamoDB use alternative models for data man- agement, such as key-value pairs or
document storage. DynamoDB enables you to offload the administrative burdens of operating and scaling a distributed
database so that you don’t have to worry about hardware provisioning, setup and configuration, replication, software
patching, or cluster scaling. Follow best practices, such as distributing data evenly, effec- tive partition and sort
keys usage, efficient data scanning, and using sparse indexes for maximizing performance and minimizing throughput
costs, when working with Amazon DynamoDB.

AWS provides several tools to help you identify those cost-saving opportunities and keep your resources right-sized. AWS
Trusted Advisor inspects your AWS environment to identify idle and underutilized resources and provides real-time
insight into service usage to help you improve system performance and save money. Amazon CloudWatch collects and tracks
metrics, monitors log files, sets alarms, and reacts to changes in AWS resources automatically. AWS Cost Explorer checks
patterns in AWS spend over time, projects future costs, identifies areas that need further inquiry, and provides
Reserved Instance recommendations.

Optimization is an ongoing process. Always stay current with the pace of AWS new releases, and assess your existing
design solutions to ensure that they remain cost-effective.

# Exam Essentials

**Know the importance of tagging.**

By using tags, you can assign metadata to AWS resources. This tagging makes it easier to manage, search for, and filter
resources in billing reports and automation activities and when setting up access controls.

**Know about various tagging tools and how to enforce the tag rules.**

With AWS Tag Editor, you can add tags to multiple resources at once, search for the resources that you want to tag, and
then add, remove, or edit tags for the resources in your search results. AWS Config identifies resources that do not
comply with tagging policies. You can use IAM policy conditions to force the usage of tags while creating the resources.

**Know the fundamental practices in reducing the usage.**

Follow the best practices of cost optimization in every step of your build process, such as turning off unused
resources, spinning up instances only when needed, and spinning them down when not in use. Use tag- ging to help with
the cost allocation. Use Amazon EC2 Spot Instances, Amazon EC2, and Reserved Instances where appropriate, and use
alerts, notifications, and cost-management tools to stay on track.

**Know the various usage patterns for right sizing.**

By understanding your business use case and backing up the analysis with performance metrics, you can choose the most
appropriate options, such as steady state; variable; predictable, but temporary; and development, test, and production
usage.

**Know the various instance families for right sizing and the corresponding use cases.**

Amazon EC2 provides a wide selection of instances to match capacity needs at the low- est cost and comes with different
options for CPU, memory, and network resources. The families include General Purpose, Compute Optimized, Memory
Optimized, Storage Optimized, and Accelerated Computing.

**Know Amazon EC2 Auto Scaling benefits and how this feature can make your solutions more optimized and highly
available.**

AWS Auto Scaling is a fast, easy way to optimize the performance and costs of your applications. It makes smart scaling
decisions based on your preferences, automatically maintains performance even when your workloads are periodic,
unpredictable, and continuously changing.

**Know how to create a single AWS Auto Scaling group to scale instances across different purchase options.**

You can provision and automatically scale Amazon EC2 capacity across different Amazon EC2 instance types, Availability
Zones, and On-Demand, Reserved Instances, and Spot purchase options in a single AWS Auto Scaling group. You can define
the desired split between On-Demand and Spot capacity, select which instance types work for your application, and
specify preferences for how Amazon EC2 Auto Scaling should distribute the AWS Auto Scaling group capacity within each
purchasing model.

**Know how block, object, and file storages are different.**

Block storage is commonly dedicated, low-latency storage for each host, and it is provisioned with each instance.
Object storage is developed for the cloud, has vast scalability, is accessed over the web, and is not directly attached
to an instance. File storage enables accessing shared files as a file system.

**Know key CloudWatch metrics available to measure the Amazon EBS efficiency and how to use them.**

CloudWatch metrics are statistical data that you can use to view, analyze, and set alarms on the operational behavior of
your volumes. Depending on your needs, set alarms and response actions that correspond to each data point. For example,
if your I/O latency is higher than you require, check the metric VolumeQueueLength to make sure that your application is
not trying to drive more IOPS than you have provisioned. Review and learn more about the available metrics that help
optimize the block storage.

**Know tools and features that help in efficient data transfer.**

Using Amazon CloudFront, you can locate data closer to users and reduce administrative efforts to minimize data transfer
costs. Amazon S3 Transfer Acceleration enables fast data transfer over an optimized network path. Use the multipart
upload file option while uploading a large file to improve network throughput.

**Know key differences between RDBMS and NoSQL databases to design efficient solutions using Amazon DynamoDB.**

Schema flexibility and the ability to store related items together make DynamoDB a solution for solving problems
associated with changing business needs and scalability issues unlike relational databases.

**Know the importance of distributing the data evenly when designing DynamoDB tables.**

Use provisioned throughput more efficiently by making the partition key more distinct. That way, data spreads throughout
the provisioned space. Use the sort key with the partition key to make a unique key to achieve better performance while
uploading data simultaneously.

**Know the different ways to read data from DynamoDB tables to avoid scans.**

DynamoDB provides Query and Scan actions to read data from a table and does not support table joins. DynamoDB provides
the GetItem action for retrieving an item by its primary key. GetItem is highly efficient because it provides direct
access to the physical location of the item. The scan always scans the entire table and can consume large amounts of
system resources.

**Know the AWS Cost Management tools and their features.**

AWS provides tools to help you manage, monitor, and, ultimately, optimize your costs. Use AWS Cost Explorer for deeper
dives into the cost drivers. Use AWS Trusted Advisor to inspect your AWS infrastructure to identify overutilized or
idle resources. AWS Budgets enables you to set custom cost and usage budgets and receive alerts when budgets approach or
exceed the limits. There are a wide range of tools to explore, such as AWS Cost Optimization – Amazon EC2 Right Sizing,
and monitoring tools to identify additional savings opportunities.

**Know how the AWS Trusted Advisor features help in saving costs and improving the performance of your solutions.**

AWS Trusted Advisor scans your AWS environment, compares it to AWS best practices, and makes recommendations for
saving money, improving system performance, and more. Cost Optimization recommendations highlight unused and
underutilized resources. Performance recommendations help to improve the speed and responsiveness of your applications.

**Know how to evaluate the reporting details in the AWS Cost Explorer default reports.**

Cost Explorer provides you with default reports: Cost and Usage reports and Reserved Instance reports. Cost and Usage
reports include your daily costs and monthly costs by service, listing the top five services. These reports help you to
determine whether you have purchased too many Reserved Instances. The Reserved Instance Coverage reports show how many
of your instance hours are covered by Reserved Instances, how much you spent on On-Demand Instances, and how much you
might have saved had you purchased more reservations. This enables you to determine whether you have under-purchased
Reserved Instances.

**Know how to extract recommendations using AWS Cost Explorer API.**

The Cost Explorer API allows you to use either AWS CLI or SDKs to query your cost and usage data. You can query for
aggregated data, such as total monthly costs or total daily usage. You can also query for granular data, such as the
number of daily write operations for DynamoDB database tables in your production environment.

**Know all of the Amazon CloudWatch metrics and how to set alarms.**

With Amazon CloudWatch, you can observe CPU utilization, network throughput, and disk I/O, and match the observed peak
metrics to a new and cheaper instance type. You choose a CloudWatch metric and threshold for the alarm to watch. The
alarm turns into the alarm state when the metric breaches the threshold for a specified number of evaluation periods.
Use the Amazon CloudWatch console, AWS CLI, or AWS SDKs for creating or managing alarms.

**Know how AWS Lambda integrates with other AWS serverless services to build cost-effective solutions.**

AWS Lambda provides the cloud-logic layer and integrates seamlessly with the other serverless services to build
virtually any type of application or backend service. For example, Amazon S3 automatically triggers Lambda functions
when an object is created, copied, or deleted. Lambda functions can process Amazon SQS messages.
