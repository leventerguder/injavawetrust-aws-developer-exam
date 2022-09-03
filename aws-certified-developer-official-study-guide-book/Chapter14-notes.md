# Stateless Application Patterns

# Introduction to the Stateless Application Pattern

Scalability is an important consideration when you create and deploy applications that are highly available, and
stateless applications are easier to scale.

When users or services interact with an application, they often perform a sequence of interactions that form a session.
A stateless application is one that requires no knowledge of previous interactions and stores no session information.
Given the same input, an application can provide the same response to any user.

A stateless application can scale horizontally because requests can be serviced by any of the available compute
resources, such as Amazon Elastic Compute Cloud (Amazon EC2) instances or AWS Lambda functions.

# Amazon DynamoDB

DynamoDB provides fast and predictable performance with seamless scalability. It enables you to offload the
administrative burdens of operating and scaling a distributed database, including hardware provisioning, setup and
configuration, replication, software patching, or cluster scaling. Also, DynamoDB offers encryption at rest, which
reduces the operational tasks and complexity involved in protecting sensitive data.

You can use global tables to keep DynamoDB tables synchronized across AWS Regions, and you can access this service using
the DynamoDB console, the AWS Command Line Interface (AWS CLI), a generic web services Application Programming
Interface (API), or any programming language that the AWS software development kit (AWS SDK) supports.

## Primary Key, Partition Key, and Sort Key

When you create a table, you must configure both the table name and the primary key of the table. The primary key
uniquely identifies each item in the table so that no two items have the same key. DynamoDB supports two different kinds
of primary keys: a partition key and sort key.

A partition key is a simple primary key, composed of only a partition key attribute. The partition key of an item is
also known as its hash attribute. The term hash attribute derives from the use of an internal hash function in DynamoDB
that evenly distributes data items across partitions based on their partition key values. DynamoDB uses the partition
key’s value as input to an internal hash function.

In a table that has only a partition key, no two items can have the same partition key value.

You can also create a primary key as a composite primary key, consisting of a partition key (first attribute) and a sort
key (second attribute).

The sort key of an item is also known as its range attribute. The term range attribute derives from the way that
DynamoDB stores items with the same partition key physically close together, in sorted order, by the sort key value.

Each primary key attribute must be a scalar, meaning that it can hold only a single value. The only data types allowed
for primary key attributes are string, number, or binary. There are no such restrictions for other, nonkey attributes.

The primary key that uniquely identifies each item in a DynamoDB table can be either simple (partition key only) or
composite (partition key combined with a sort key). Partition key values determine the logical partitions in which a
table’s data is stored, which affects the table’s underlying physical partitions. Efficient partition key design keeps
your workload spread evenly across these partitions.

## Using Write Shards to Distribute Workloads Evenly

A shard is a uniquely identified group of stream records within a stream. To distribute writes better across a partition
key space in DynamoDB, expand the space. You can add a random number to the partition key values to distribute the items
among partitions, or you can use a number that is calculated based on what you want to query

## Amazon DynamoDB Tables

DynamoDB global tables provide a fully managed solution for deploying a multiregion, multi-master database, without
having to build and maintain your own replication solution. When you create a global table, you configure the AWS
Regions where you want the table to be available. DynamoDB performs all of the necessary tasks to create identical
tables in these regions and propagate ongoing data changes to all of the regions.

DynamoDB global tables are ideal for massively scaled applications, with globally dispersed users. In such an
environment, you can expect fast application performance. Global tables provide automatic multi-master replication to
AWS Regions worldwide, so you can deliver low-latency data access to your users no matter where they are located.

## Provisioned Throughput

With DynamoDB, you can create database tables that store and retrieve any amount of data and serve any level of request
traffic. You can scale your table’s throughput capacity up or down without downtime or performance degradation, and
you can use the AWS Management Console to monitor resource utilization and performance metrics.

For any table or global secondary index, the minimum settings for provisioned throughput are one read capacity unit
and one write capacity unit.

You can apply all of the available throughput of an account to a single table or across multiple tables.

## Requesting Throttle and Burst Capacity

If your application performs reads or writes at a higher rate than your table can support, DynamoDB begins to throttle
those requests. When DynamoDB throttles a read or write, it returns a ProvisionedThroughputExceededException to the
caller. The application can then take appropriate action, such as waiting for a short interval before retrying the
request.

The AWS SDKs provide built-in support for retrying throttled requests; you do not need to write this logic yourself. The
DynamoDB console displays CloudWatch metrics for your tables so that you can monitor throttled read requests and write
requests. If you encounter excessive throttling, consider increasing your table’s provisioned throughput settings.

In some cases, DynamoDB uses burst capacity to accommodate reads or writes in excess of your table’s throughput
settings. With burst capacity, unexpected read or write requests can succeed where they otherwise would be throttled.
Burst capacity is available on a best effort basis, and DynamoDB does not verify that this capacity is always
available.

## Amazon DynamoDB Secondary Indexes: Global and Local

A secondary index is a data structure that contains a subset of attributes from a table. The index uses an alternate key
to support Query operations in addition to making queries against the primary key. You can retrieve data from the index
using a Query. A table can have multiple secondary indexes, which give your applications access to many different Query
patterns.

You can create one or more secondary indexes on a table. DynamoDB does not require indexes, but indexes give your
applications more flexibility when you query your data. After you create a secondary index on a table, you can read or
scan data from the index in much the same way as you do from the table.

DynamoDB supports the following kinds of indexes:

Global secondary index A global secondary index is one with a partition key and sort key that can be different from
those on the table.

Local secondary index A local secondary index is one that has the same partition key as the table but a different sort
key.

You can define up to five global secondary indexes and five local secondary indexes per table. You can also scan an
index as you would a table.

When you create an index, you define an alternate key (partition key and sort key) for the index. You also define the
attributes that you want to project from the base table into the index. DynamoDB copies these attributes into the index
along with the primary key attributes from the base table. You can Query or Scan the index like a table.

# Amazon DynamoDB Streams

Amazon DynamoDB Streams captures data modification events in DynamoDB tables. The data about these events appear in the
stream in near real time and in the order that the events occurred.

Each event represents a stream record. When you enable a stream on a table, DynamoDB captures information about every
modification to data items in the table.

A stream record contains information about a data modification to a single item in a DynamoDB table including the
primary key attributes of the items.

Stream records have a lifetime of 24 hours, after which they are deleted automatically from the stream.

A DynamoDB stream is a time-ordered flow of information of item-level modifications (create, update, or delete) to items
in a DynamoDB table.

DynamoDB Streams does the following:

- Each stream record appears exactly once in the stream.
- For each item that is modified in a DynamoDB table, the stream records appear in the same sequence as the actual
  modifications to the item.

## DynamoDB Cross-Region Replication

You can create tables that automatically replicate across two or more AWS Regions with full support for multi-master
writes. Using cross-region replication, you can build fast, massively scaled applications for a global user base without
having to manage the replication process.

## DynamoDB Stream Endpoints

AWS maintains separate endpoints for DynamoDB and DynamoDB Streams. To work with database tables and indexes, your
application must access a DynamoDB endpoint.

## AWS Lambda Triggers in DynamoDB Streams

DynamoDB integrates with AWS Lambda, so you can create triggers (code that executes automatically) that automatically
respond to events in DynamoDB Streams. With triggers, you can build applications that react to data modifications in
DynamoDB tables.

## Amazon DynamoDB Auto Scaling

Amazon DynamoDB automatic scaling actively manages throughput capacity for tables and global secondary indexes. With
automatic scaling, you can define a range (upper and lower limits) for read and write capacity units and define a target
utilization percentage within that range. DynamoDB automatic scaling seeks to maintain your target utilization, even as
your application workload increases or decreases.

## Burst Capacity

DynamoDB provides some flexibility in your per-partition throughput provisioning by providing burst capacity.

DynamoDB currently retains up to 5 minutes (300 seconds) of unused read and write capacity.

To enable DynamoDB automatic scaling, you create a scaling policy. This scaling policy specifies the table or global
secondary index that you want to manage, which capacity type to manage (read or write capacity), the upper and lower
boundaries for the provisioned throughput settings, and your target utilization.

When you create a scaling policy, Application Auto Scaling creates a pair of CloudWatch alarms on your behalf. Each pair
represents your upper and lower boundaries for provisioned throughput settings. These CloudWatch alarms are triggered
when the table’s actual utilization deviates from your target utilization for a sustained period of time.

## Optimistic Locking with Version Number

Optimistic locking is a strategy to ensure that the client-side item that you are updating or deleting is the same as
the item in DynamoDB. If you use this strategy, then all writes on your database are protected from being accidentally
overwritten.

## DynamoDB Tags

You can label DynamoDB resources with tags. Tags allow you to categorize your resources in different ways: by purpose,
owner, environment, or other criteria. Tags help you to identify a resource quickly based on the tags that you have
assigned to it, and they help you to see your AWS bills broken down by tags.

## DynamoDB Items

A DynamoDB item is a collection of attributes that is uniquely identifiable among all other entities in the table, and
each item has a name and a value. An attribute value can be a scalar, a set, or a document type.

## On-Demand Backup and Restore

You can create on-demand backups and enable point-in-time recovery for your DynamoDB tables. DynamoDB on-demand backups
enable you to create full backups of your tables for long-term retention and archival for regulatory compliance.

In addition, on-demand backup and restore operations do not affect performance or API latencies. Backups are preserved
regardless of table deletion. You can create table backups using the console, the AWS CLI, or the DynamoDB API.

## Point-in-Time Recovery

You can enable point-in-time recovery (PITR) and create on-demand backups for your DynamoDB tables. Point-in-time
recovery helps protect your DynamoDB tables from accidental write or delete operations. With point-in-time recovery,
you do not have to worry about creating, maintaining, or scheduling on-demand backups. DynamoDB maintains incremental
backups of your table. In addition, point-in-time operations do not affect performance or API latencies. You can enable
point-in-time recovery using the AWS Management Console, AWS CLI, or the DynamoDB API.

# Amazon ElastiCache

Amazon ElastiCache is a web service that makes it easy to set up, manage, and scale distributed in-memory cache
environments on the AWS Cloud. It provides a high- performance, resizable, and cost-effective in-memory cache while
removing the complexity associated with deploying and managing a distributed cache environment.

You can use ElastiCache to store the application state. Applications often store session data in memory, but this
approach does not scale well.

You can use ElastiCache to store the application state. Applications often store session data in memory, but this
approach does not scale well. To address scalability and provide a shared data storage for sessions that can be
accessible from any individual web server, abstract the HTTP sessions from the web servers themselves. A common solution
is to leverage an in-memory key-value store. ElastiCache supports the following open-source in-memory caching engines:

- Memcached is an open source, high-performance, distributed memory object caching system that is widely adopted by and
  protocol-compliant with ElastiCache.
- Redis is an open source, in-memory data structure store that you can use as a database cache and message broker.
  ElastiCache supports Master/Slave replication and Multi- AZ replication that you can use to achieve cross-Availability
  Zone redundancy.

ElastiCache is an in-memory cache. Caching frequently used data is one of the most important performance optimizations
that you can make in your applications. Compared to retrieving data from an in-memory cache, querying a database is a
much more expensive operation. By storing frequently accessed data in-memory, you can greatly improve the speed and
responsiveness of read-intensive applications.

## Considerations for Choosing a Distributed Cache

In a distributed session cache, the sessions are divided by the number of nodes in the cache cluster. In the event of a
failure, only the sessions that are stored on the failed node are affected.
If reducing risk is more important than cost, adding additional nodes to reduce further the percentage of stored
sessions on each node may be ideal even when fewer nodes are sufficient.

There are a number of ways to store sessions in key-value stores. Many application frameworks provide libraries that can
abstract some of the integration required to Get/Set those sessions in memory. In other cases, you can write your own
session handler to persist the sessions directly.

Use Memcached if you require the following:

- Use a simple data model
- Run large nodes with multiple cores or threads
- Scale out or scale in
- Partition data across multiple shards
- Cache objects, such as a database

Use Redis if you require the following:

- Work with complex data types
- Sort or rank in-memory datasets
- Persist the key store
- Replicate data from the primary to one or more read replicas for read-intensive applications
- Automate failover if the primary node fails
- Publish and subscribe (pub/sub): the client is informed of events on the server
- Back up and restore data

![](Memcached-or-Redis.png)

## ElastiCache Terminology

This section describes some of the key terminology that ElastiCache uses.

## Nodes

A node is the smallest building block of an ElastiCache deployment. A node is a fixed-size chunk of secure,
network-attached RAM. Each node runs an instance of Memcached or Redis, depending on which you select when you create
the cluster.

## Clusters

Each ElastiCache deployment consists of one or more nodes in a cluster. When you create a cluster, you may choose from
many different nodes based on the requirements of both your solution case and your capacity. One Memcached cluster can
be as large as 20 nodes. Redis clusters consist of a single node; however, you can group multiple clusters into a Redis
replication group.

**Replication group**

A replication group is a collection of Redis clusters with one primary read/write cluster and up to five secondary,
read-only clusters called read replicas.

Each read replica maintains a copy of the data from the primary cluster. Asynchronous replication mechanisms keep the
read replicas synchronized with the primary cluster. Applications can read from any cluster in the replication group.
Applications can write only to the primary cluster. Read replicas enhance scalability and guard against data loss.

**Endpoint**

An endpoint is the unique address your application uses to connect to an ElastiCache node or cluster. Memcached and
Redis have the following characteristics with respect to endpoints:

- A Memcached cluster has its own endpoint and a configuration endpoint.
- A standalone Redis cluster has an endpoint to connect to the cluster for both reads and writes.
- A Redis replication group has two types of endpoints.
    - The primary endpoint connects to the primary cluster in the replication group.
    - The read endpoint points to a specific cluster in the replication group.

## Cache Scenarios

ElastiCache caches data as key-value pairs. An application can retrieve a value corresponding to a specific key. An
application can store an item in cache by a specific key, value, and an expiration time. Time to live (TTL) is an
integer value that specifies the number of seconds until the key expires.

A cache hit occurs when an application requests data from the cache, the data is both present and not expired in the
cache, and it returns to the application. A cache miss occurs if an application requests data from the cache, and it is
not present in the cache (returning a null). In this case, the application requests and receives the data from the
database and then writes the data to the cache.

### Strategies for Caching

The strategy or strategies that you want to implement for populating and maintaining your cache depend on what data you
are caching and the access patterns to that data. For example, you would likely not want to use the same strategy for a
top-10 leaderboard on a gaming site, Facebook posts, and trending news stories.

**Lazy Loading**

Lazy loading loads data into the cache only when necessary. Whenever your application requests data, it first makes the
request to the ElastiCache cache. If the data exists in the cache and it is current, ElastiCache returns the data to
your application. If the data does not exist in the cache or the data in the cache has expired, your application
requests the data from your data store, which returns the data to your application. Your application then writes the
data received from the store to the cache so that it can be retrieved more quickly the next time that it is requested.

**Advantages of Lazy Loading**

- Only requested data is cached.
    - Because most data is never requested, lazy loading avoids filling up the cache with data that is not requested.
- Node failures are not fatal.
    - When a new, empty node replaces a failed node, the application continues to function, though with increased
      latency. As requests are made to the new node, each missed cache results in a query of the database and adding the
      data copy to the cache so that subsequent requests are retrieved from the cache.

**Disadvantages of Lazy Loading**

- There is a cache miss penalty.
    - Each cache miss results in three trips:
        - Initial request for data from the cache
        - Querying of the database for the data
        - Writing the data to the cache
    - This can cause a noticeable delay in data getting to the application.
- Stale Data
    - The application may receive stale data because another application may have updated the data in the database
      behind the scenes.

**Write-Through**

The write-through strategy adds data or updates data in the cache whenever data is written to the database.

**Advantages of Write-Through**

- The data in the cache is never stale.
    - Because the data in the cache updates every time it is written to the database, the data in the cache is always
      current.

**Disadvantages of Write-Through**

- Write Penalty
    - Every write involves two trips: a write to the cache and a write to the database.
- Missing Data
    - When a new node is created either to scale up or replace a failed node, the node does not contain all data. Data
      continues to be missing until it is added or updated in the database. In this scenario, you might choose to use a
      lazy caching approach to repopulate the cache.
- Unused data
    - Because most data is never read, there can be a lot of data in the cluster that is never read.
- Cache churn
    - The cache may be updated often if certain records are updated repeatedly.

## Data Access Patterns

Retrieving a flat key from an in-memory cache is faster than the most performance-tuned database query. Analyze the
access pattern of the data before you determine whether you should store it in an in-memory cache.

## Scaling Your Environment

As your workloads evolve over time, you can use ElastiCache to change the size of your environment to meet the
requirements of your workloads. To meet increased levels of write or read performance, expand your cluster horizontally
by adding cache nodes. To scale your cache vertically, select a different cache node type.

**Scale horizontally**

ElastiCache functionality enables you to scale the size of your cache environment horizontally. This functionality
differs depending on the cache engine you select. With Memcached, you can partition your data and scale horizontally to
20 nodes or more. A Redis cluster consists of a single cache node that handles read and write trans- actions. You can
create additional clusters to include a Redis replication group. Although you can have only one node handle write
commands, you can have up to five read replicas handle read-only requests.

**Scale vertically**

The ElastiCache service does not directly support vertical scaling of your cluster. You can create a new cluster with
the desired cache node types and begin redirecting traffic to the new cluster.

## Replication and Multi-AZ

Replication is an effective method for providing speedy recovery if a node fails and for serving high quantities of read
queries beyond the capacities of a single node. ElastiCache clusters running Redis support both. In contrast, cache
clusters running Memcached are standalone in-memory services that do not provide any data redundancy-protection
services. Cache clusters running Redis support the notion of replication groups. A replication group consists of up to
six clusters, with five of them designated as read replicas. By using a replication group, you can scale horizontally by
developing code in the application to offload reads to one of the five replicas.

## Backup and Recovery

ElastiCache clusters that run Redis support snapshots. Use snapshots to persist your data from your in-memory key-value
stores to disk. Each snapshot is a full clone of the data that you can use to recover to a specific point in time or to
create a copy for other purposes. Snapshots are not available to clusters that use the Memcached caching engine. This is
because Memcached is a purely in-memory, key-value store, and it always starts empty. ElastiCache uses the native backup
capabilities of Redis and generates a standard Redis database backup file, which is stored in Amazon S3.

## Control Access

The primary way to configure access to your ElastiCache cluster is by restricting connectivity to your cluster through
a security group. You can define a security group and add one or more inbound rules that restrict the source traffic.
When a cache cluster is deployed inside a virtual private cloud, every node is assigned a private IP address within one
or more subnets that you choose.

You cannot access individual nodes from the internet or from Amazon EC2 instances outside of the Amazon Virtual Private
Cloud (Amazon VPC).

ou can use the access control lists (ACLs) to constrain network inbound traffic.

Access to manage the configuration and infrastructure of the cluster is controlled separately from access to the
actual Memcached or Redis service endpoint. Using the IAM service, you can define policies that control which AWS users
can manage the ElastiCache infrastructure.

The ability to configure the cluster and govern the infrastructure is handled independently from access to the actual
cache cluster endpoint, which is managed by using the IAM service. Using IAM, you can set up policies that determine
which users can manage the ElastiCache infrastructure

# Amazon S3 Core Concepts

Amazon S3 is a stateless application that does not save client data that generates in one session for use in the next
session with that client. Each session starts as if it was the first time, and responses are not dependent on data from
a previous session. This means that the server does not store any state about the client session. Instead, the session
data is stored on the client and passed to the server as requested.

## Buckets

A bucket is a container for objects stored in Amazon S3. Every object is contained in a bucket.

Buckets serve several purposes:

- They organize the Amazon S3 namespace at the highest level.
- They identify the account responsible for storage and data transfer charges.
- They play a role in access control.
- They serve as the unit of aggregation for usage reporting.

## Creating a Bucket

Amazon S3 provides APIs for creating and managing buckets. By default, you can create up to 100 buckets in each of your
accounts. If you need more buckets, increase your bucket limit by submitting a service limit increase.

When you create a bucket, provide a name for the bucket, and then choose the AWS Region where you want to create the
bucket. You can store any number of objects in a bucket.

**Objects**

Objects are the principal items stored in Amazon S3. Objects consist of object data and metadata. The data part is
opaque to Amazon S3. The metadata is a set of name-value pairs that characterize the object. These include certain
default metadata, such as the date last modified and standard HTTP metadata, such as Content-Type. It is also possible
for you to configure custom metadata at the time of object creation.

**Keys**

A key is the unique identifier for an object within a bucket. Every object in a bucket has exactly one key. Because the
combination of a bucket, key, and version ID uniquely identifies each object, Amazon S3 is like a basic data map between
bucket + key + version and the object itself.

**Versioning**

Versioning is a way to keep multiple variations of an object in the same bucket. You can use versioning to preserve,
retrieve, and restore every version of every object stored in your Amazon S3 bucket. With versioning, you can recover
from both unintended user actions and application failures.

Versioning-enabled buckets allow you to recover objects from accidental deletion or overwrite.

## Accessing a Bucket

Use the Amazon S3 console to access your bucket. You can perform almost all bucket operations without having to write
any code. If you access a bucket programmatically, Amazon S3 supports the RESTful architecture wherein your buckets and
objects are resources, each with a resource Uniform Resource Identifier (URI) that uniquely identifies the resource.

## Bucket Restrictions and Limitations

By default, you can create up to 100 buckets in each of your accounts. If you need additional buckets, increase your
bucket limit by submitting a service limit increase.

- Bucket ownership is not transferable; however, if a bucket is empty, you can delete it.
- There is no limit to the number of objects that you can store in a bucket and no difference in performance whether
  you use many buckets or only a few.
- You cannot create a bucket within another bucket.
- The high-availability engineering of Amazon S3 is focused on GET, PUT, LIST, and DELETE operations.

## Rules for Naming Buckets

After you create an S3 bucket, you cannot change the bucket name, so choose the name wisely.

The following are the rules for naming S3 buckets in all AWS Regions:

- Bucket names must be unique across all existing bucket names in Amazon S3.
- Bucket names must comply with DNS naming conventions.
- Bucket names must be between 3 and 63 characters long.
- Bucket names must not contain uppercase characters or underscores.
- Bucket names must start with a lowercase letter or number.
- Bucket names must be a series of one or more labels. Use a single period (.) to separate adjacent labels. Bucket names
  can contain lowercase letters, numbers, and hyphens. Each label must start and end with a lowercase letter or a
  number.
- Bucket names must not be formatted as an IP address (for example, 192.168.4.5).

## Working with Amazon S3 Buckets

Amazon S3 is cloud storage for the internet. To upload your data, such as images, videos, and documents, you must first
create a bucket in one of the AWS Regions. You can then upload any number of objects to the bucket.

An Amazon S3 bucket name is globally unique regardless of the AWS Region in which you create the bucket. Configure the
name at the time that you create the bucket. Amazon S3 creates buckets in a region that you choose. To minimize latency,
reduce costs, or address regulatory requirements, choose any AWS Region that is geographically close to you.

## Object Lifecycle Management

To manage your objects so that they are stored cost-effectively throughout their life, configure their lifecycle
policy. A lifecycle policy is a set of rules that designates actions that Amazon S3 applies to a group of objects. There
are two types of actions:

**Transition actions**

Designate when objects transition from one storage class to another. For instance, you might decide to transition
objects to the STANDARD_IA storage class 45 days after you created them, or archive objects to the GLACIER storage class
six months after you created them.

**Expiration actions**

Designate when objects expire. Amazon S3 deletes expired objects on your behalf.

## Bucket Policies

Bucket policies are a centralized way to control access to buckets and objects based on numerous conditions, such as
operations, requesters, resources, and aspects of the request. The policies are written using the IAM policy language
and enable centralized management of permissions.

## Amazon S3 Storage Classes

Amazon S3 offers a variety of storage classes devised for different scenarios. Among these storage classes are Amazon S3
STANDARD for general-purpose storage of frequently accessed data; Amazon S3 STANDARD_IA (Infrequent Access) for
long-lived, but less frequently accessed data; and GLACIER for long-term archival purposes.

### Storage Classes for Frequently Accessed Objects

Amazon S3 provides storage classes for performance-sensitive use cases (millisecond access time) and frequently accessed
data. Amazon S3 provides the following storage classes:

**STANDARD**

Standard is the default storage class. If you do not specify the storage class when uploading an object, Amazon S3
assigns the STANDARD storage class.

**REDUCED_REDUNDANCY**

The Reduced Redundancy Storage (RRS) storage class is designed for noncritical, reproducible data that you can store
with less redundancy than the STANDARD storage class.

### Storage Classes for Infrequently Accessed Objects

The STANDARD_IA and ONEZONE_IA storage classes are designed for data that is long-lived and infrequently accessed.
STANDARD_IA and ONEZONE_IA objects are available for millisecond access (similar to the STANDARD storage class). Amazon
S3 charges a fee for retrieving these objects; thus, they are most appropriate for infrequently accessed data.

Possible use cases for STANDARD_IA and ONEZONE_IA are as follows:

- For storing backups
- For older data that is accessed infrequently but that still requires millisecond access

**STANDARD_IA**

Objects stored using this storage class are stored redundantly across multiple, geographically distinct Availability
Zones (similar to the STANDARD storage class). STANDARD_IA objects are resilient to data loss of an Availability Zone.
This storage class provides more availability, durability, and resiliency than the ONEZONE_IA class.

**ONEZONE_IA**

Amazon S3 stores the object data in only one Availability Zone, which makes it less expensive than STANDARD_IA. However,
the data is not resilient to the physical loss of the Availability Zone resulting from disasters, such as earthquakes
and floods. The ONEZONE_IA storage class is as durable as STANDARD_IA, but it is less available and less resilient.

To determine when to use a particular storage class, follow these recommendations:

**STANDARD_IA**

Use for your primary copy (or only copy) of data that cannot be regenerated.

### GLACIER Storage Class

You use the GLACIER storage class to archive data where access is infrequent. Objects that you archive are not available
for real-time access. The GLACIER storage class offers the same durability and resiliency as the STANDARD storage class.

When you store objects in Amazon S3 with the GLACIER storage class, Amazon S3 uses the low-cost Amazon Simple Storage
Service Glacier (Amazon S3 Glacier) service to store these objects. Though the objects are stored in Amazon S3 Glacier,
these remain Amazon S3 objects that are managed in Amazon S3, and they cannot be accessed directly through Amazon S3
Glacier.

At the time that you create an object, it is not possible to specify GLACIER as the stor- age class. The way that
GLACIER objects are created is by uploading objects first using STANDARD as the storage class. You can transition these
objects to the GLACIER storage class by using lifecycle management.

### Setting the Storage Class of an Object

Amazon S3 APIs offer support for setting or updating the storage class of objects. When you create a new object,
configure its storage class. For example, when you create objects with the PUT Object, POST Object, and Initiate
Multipart Upload APIs, add the x-amz-storageclass request header to configure a storage class. If you do not add this
header, Amazon S3 uses STANDARD, the default storage class.

## Amazon S3 Default Encryption for S3 Buckets

Amazon S3 default encryption provides a way to set the default encryption behavior for an Amazon S3 bucket. You can set
default encryption on a bucket so that all objects are encrypted when they are stored in the bucket. The objects are
encrypted using server-side encryption with either Amazon S3 managed keys (SSE-S3) or AWS KMS managed keys (SSE-KMS).

When you use server-side encryption, Amazon S3 encrypts an object before saving it to disk in its data centers and then
decrypts the object when you download it.

### Protecting Data Using Encryption

Data protection refers to protecting data while in transit (as it travels to and from Amazon S3), and at rest (while it
is stored on disks in Amazon S3 data centers). You can protect data in transit by using SSL or by using client-side
encryption with the following options of protecting data at rest in Amazon S3:

**Use server-side encryption**

You request Amazon S3 to encrypt your object before saving it on disks in its data centers
and then decrypt the object when you download it.

**Use client-side encryption**

You can encrypt data on the client side and upload the encrypted data to Amazon S3 and then
manage the encryption process, the encryption keys, and related tools

### Protecting Data Using Server-Side Encryption

Server-side encryption is about data encryption at rest; that is, Amazon S3 encrypts your data at the object level as it
writes it to disks in its data centers and decrypts it for you when you access it. As long as you authenticate your
request and you have access permissions, there is no difference in the way that you access encrypted or unencrypted
objects. For example, if you share your objects using a presigned URL, that URL works the same way for both encrypted
and unencrypted objects.

**Use server-side encryption with Amazon S3 Managed Keys (SSE-S3)**

Each object is encrypted with a unique key employing strong multifactor encryption. As an additional safeguard, it
encrypts the key itself with a master key that it regularly rotates. Amazon S3 server-side encryption uses one of the
strongest block ciphers available, 256-bit Advanced Encryption Standard (AES-256), to encrypt your data.

SSE-KMS also provides you with an audit trail of when your key was used and by whom. Additionally, you can create and
manage encryption keys yourself or use a default key that is unique to you, the service you are using, and the region in
which you are working.

**Use server-side encryption with customer-provided keys (SSE-C)**

You manage the encryption keys, and Amazon S3 manages the encryption as it writes to disks. You also manage decryption
when you access your objects.

## Working with Amazon S3 Objects

Amazon S3 is a simple key-value store designed to store as many objects as you want. Store these objects in one or more
buckets. An object consists of the following:

**Key**

The key is the name that you assign to an object. The object key is used to retrieve the object.

**Version ID**

Within a bucket, a key and version ID uniquely identify an object. The version ID is a string that Amazon S3 generates
when you add an object to a bucket.

**Value**

The information being stored. An object value can be any sequence of bytes. Objects can range in size from 0 to 5
terabytes (TB).

**Metadata**

A set of key-value pairs with which you can store information about the object. You can assign metadata, referred to as
user-defined metadata, to your objects in Amazon S3. Amazon S3 also assigns system metadata to these objects, which it
uses for managing objects.

**Subresources**

Amazon S3 uses the subresource mechanism to store object-specific additional information. Because subresources are
subordinates to objects, they are always associated with an entity, such as an object or a bucket.

**Access control information**

You can control access to the objects that you store in Amazon S3. Amazon S3 supports both the resource-based access
control, such as an access control list (ACL) and bucket policies, and user-based access control.

## Object Keys and Metadata

Each Amazon S3 object is composed of several parts. These parts include the data, a key, and metadata. An object key (or
key name) uniquely identifies the object in a bucket. Object metadata is a set of name-value pairs. You can set the
object metadata at the time that you upload an object. However, after you upload the object, you cannot modify object
metadata. The only way to modify object metadata after it has been uploaded is to create a copy of the object.

### Uploading Objects

Depending on the size of the data that you are uploading, Amazon S3 provides the following options:

**Upload objects in a single operation**

Use a single PUT operation to upload objects up to 5 GB in size. For objects that are up to 5 TB in size, use the
multipart upload API.

**Upload objects in parts**

The multipart upload API is designed to improve the upload experience for larger objects. Upload these object parts
independently, in any order, and in parallel.

## Deleting Objects from a Version-Enabled Bucket

If your bucket is version-enabled, then multiple versions of the same object can exist in the bucket. When working with
version-enabled buckets, the DELETE API enables the following options:

**Specify a nonversioned delete request**

Specify only the object’s key, not the version ID. In this case, Amazon S3 creates a delete marker and returns its
version ID in the response. This makes your object disappear from the bucket.

**Specify a versioned delete request**

Specify both the key and a version ID. In this case, the following two outcomes are possible:

- If the version ID maps to a specific object version, then Amazon S3 deletes the specific version of the object.
- If the version ID maps to the delete marker of that object, Amazon S3 deletes the delete marker. This causes the
  object to reappear in your bucket.

# Amazon Elastic File System

Amazon Elastic File System (Amazon EFS) provides simple, scalable file storage for use with Amazon EC2. With Amazon EFS,
storage capacity is elastic, growing and shrinking automatically as you add and remove files so your applications have
the storage they need when they need it.

Amazon EFS supports the Network File System versions 4.0 and 4.1 (NFSv4) proto-
col, so the applications and tools that you use today work seamlessly with Amazon EFS. Multiple Amazon EC2 instances can
access an Amazon EFS file system at the same time, providing a common data source for workloads and applications running
on more than one instance or server.

The service is highly scalable, highly available, and highly durable. Amazon EFS stores data and metadata across
multiple Availability Zones in a region, and it can grow to petabyte scale, drive high levels of throughput, and allow
massively parallel access from Amazon EC2 instances to your data.

Amazon EFS supports two forms of encryption for file systems: encryption in transit and encryption at rest. You can
enable encryption at rest when creating an Amazon EFS file system. If you do, all of your data and metadata is
encrypted. You can enable encryption in transit when you mount the file system.

Amazon EFS is designed to provide the throughput, input/output operations per sec- ond (IOPS), and low latency needed
for a broad range of workloads. With Amazon EFS, throughput and IOPS scale as a file system grows, and file operations
are delivered with consistent, low latencies.

## How Amazon EFS Works

Amazon EFS provides file storage in the AWS Cloud. With Amazon EFS, you can create a file system, mount the file system
on an Amazon EC2 instance, and then read and write data to and from your file system. You can mount an Amazon EFS file
system in your VPC through the NFSv4 protocol.

You can access your Amazon EFS file system concurrently from Amazon EC2 instances in your Amazon VPC so that
applications that scale beyond a single connection can access a file system. Amazon EC2 instances running in multiple
Availability Zones within the same region can access the file system so that many users can access and share a common
data source.

However, there are restrictions. You can mount an Amazon EFS file system on instances in only one VPC at a time. Both
the file system and VPC must be in the same AWS Region.

To access your Amazon EFS file system in a VPC, create one or more mount targets in the VPC. A mount target provides an
IP address for an NFSv4 endpoint at which you can mount an Amazon EFS file system.

### How Amazon EFS Works with AWS Direct Connect

Using an Amazon EFS file system mounted on an on-premises server, you can migrate on- premises data into the AWS Cloud
hosted in an Amazon EFS file system. You can also take advantage of bursting. This means that you can move data from
your on-premises servers into Amazon EFS, analyze it on a fleet of Amazon EC2 instances in your Amazon VPC, and then
store the results permanently in your file system or move the results back to your on-premises server.

In Amazon EFS, a file system is the primary resource. Each file system has properties such as ID, creation token,
creation time, file system size in bytes, number of mount targets created for the file system, and the file system
state.

## Creating an IAM User

Services in AWS, such as Amazon EFS, require that you provide credentials when you access them so that the service can
determine whether you have permissions to access its resources. AWS recommends that you do not use the AWS account
credentials of your account to make requests. Instead, create an IAM user, and grant that user full access. AWS refers
to these users as administrators. You can use the administrator credentials, instead of AWS account credentials, to
interact with AWS and perform tasks, such as creating a bucket, creating users, and granting them permissions.

## Creating a File System

You can use the Amazon EFS console, or the AWS CLI, to create a file system. You can also use the AWS SDKs to create
file systems programmatically.

## Using File Systems

Amazon EFS presents a standard file system interface that supports semantics for full
file system access. Using NFSv4.1, you can mount your Amazon EFS file system on any Amazon EC2 Linux-based instance.
Once mounted, you can work with the files and directories as you would with a local file system. You can also use AWS
DataSync to copy files from any file system to Amazon EFS.

## Managing Access to Encrypted File Systems

Using Amazon EFS, you can create encrypted file systems. Amazon EFS supports two forms of encryption for file systems:
encryption in transit and encryption at rest. Any key management that you must perform is related only to encryption at
rest. Amazon EFS auto- matically manages the keys for encryption in transit. If you create a file system that uses
encryption at rest, data and metadata are encrypted at rest.

Amazon EFS uses AWS KMS for key management. When you create a file system using encryption at rest, specify a customer
master key (CMK). The CMK can be aws/elasticfilesystem (the AWS managed CMK for Amazon EFS), or it can be a CMK that you
manage. File data, the contents of your files, is encrypted at rest using the CMK that you specified when you created
your file system.

## Amazon EFS Performance

Amazon EFS file systems are spread across an unconstrained number of storage servers, allowing file systems to expand
elastically to petabyte scale. The distribution also allows them to support massively parallel access from Amazon EC2
instances to your data. Because of this distributed design, Amazon EFS avoids the bottlenecks and limitations inherent
to conventional file servers.

Amazon EFS data is distributed across multiple Availability Zones, providing a high level of availability and
durability.

### Performance Modes

**General Purpose performance mode**

AWS recommends the General Purpose performance mode for the majority of your Amazon EFS file systems. General Purpose is
ideal for latency-sensitive use cases, such as web serving environments, content management systems, home directories,
and general file serving. If you do not choose a performance mode when you create your file system, Amazon EFS selects
the General Purpose mode for you by default.

**Max I/O performance mode**

File systems in the Max I/O mode can scale to higher levels of aggregate throughput and operations per second with a
trade-off of slightly higher latencies for file operations. Highly parallelized applications and workloads, such as
big data analysis, media processing, and genomics analysis can benefit from this mode.

## Throughput Scaling in Amazon EFS

Throughput on Amazon EFS scales as a file system grows. Because file-based workloads are typically spiky, driving high
levels of throughput for short periods of time and low levels of throughput the rest of the time, Amazon EFS is designed
to burst to high throughput levels for periods of time.

All file systems, regardless of size, can burst to 100 MB/s of throughput, and those larger than 1 TB can burst to 100
MB/s per TB of data stored in the file system. For exam- ple, a 10-TB file system can burst to 1,000 MB/s of
throughput (10 TB × 100 MB/s/TB). The portion of time a file system can burst is determined by its size, and the
bursting model is designed so that typical file system workloads will be able to burst virtually any time they need to.

Amazon EFS uses a credit system to determine when file systems can burst. Each file system earns credits over time at a
baseline rate that is determined by the size of the file sys- tem, and it uses credits whenever it reads or writes data.
The baseline rate is 50 MB/s per TB of storage (equivalently, 50 KB/s per GB of storage).

# Summary

In this chapter, stateless applications are defined as those that do not require knowledge of previous individual
interactions and do not store session information locally. Stateless application design is beneficial because it reduces
the risk of loss of session information or critical data. It also improves user experience by reducing the chances that
context-specific data is lost if a resource containing session information becomes unavailable. To accomplish this,
AWS customers can use Amazon DynamoDB, Amazon ElastiCache, Amazon Simple Storage Service (Amazon S3), and Amazon Elastic
File System (Amazon EFS)

DynamoDB is a fast and flexible NoSQL database service that is used by applications that require consistent,
single-digit millisecond latency at any scale. In stateless applica- tion design, you can use DynamoDB to store and
rapidly retrieve session information. This separates session information from application resources responsible for
processing user interactions. For example, a web application can use DynamoDB to store user shopping carts. If an
application server becomes unavailable, the users accessing the application do not experience a loss of service.

To further improve speed of access, DynamoDB supports global secondary indexes and local secondary indexes. A secondary
index contains a subset of attributes from a table and uses an alternate key to support custom queries. A local
secondary index has the same partition key as a table but uses a different sort key. A global secondary index has
different partition and sort keys.

DynamoDB uses read and write capacity units to determine cost. A single read capacity unit represents one strongly
consistent read per second (or two eventually consistent reads per second) for items up to 4 KB in size. A single write
capacity unit represents one write per second for items up to 1 KB in size. Items larger than these values consume
additional read or write capacity.

ElastiCache enables you to quickly deploy, manage, and scale distributed in- memory cache environments. With
ElastiCache, you can store application state information in a shared location by using an in-memory key-value store.
Caches can be created using either Memcached or Redis caching engines. Read and write operations to a backend database
can be time-consuming. Thus, ElastiCache is especially effective as a caching layer for heavy-use applications that
require rapid access to backend data. You can also use ElastiCache to store HTTP sessions, further improving the
performance of your applications.

ElastiCache offers various scalability configurations that improve access times and avail- ability. For example,
read-heavy applications can use additional cache cluster nodes to respond to queries. Should there be an increase in
demand, additional cluster nodes can be scaled out quickly.

There are some differences between the available caching engines. AWS recommends that you use Memcached for simple data
models that may require scaling and partitioning/ sharding. Redis is recommended for more complex data types, persistent
key stores, read- replication, and publish/subscribe operations.

In certain situations, storing state information can involve larger file operations (such as file uploads and batch
processes). Amazon S3 can support millions of operations per second on trillions of objects through a simple web
service. Through simple integration, developers can take advantage of the massive scale of object storage.

Amazon S3 stores objects in buckets, which are addressable using unique URLs (such
as http://johnstiles.s3.amazonaws.com/). Buckets enable you to group similar objects and configure access control
policies for internal and external users. Buckets also serve as the unit of aggregation for usage reporting. There is no
limit to the number of objects that can be stored in a bucket, and there is no performance difference between using one
or multiple buckets for your web application. The decision to use one or more buckets is often a consideration of
access control.

Amazon S3 buckets support versioning and lifecycle configurations to maintain the integrity of objects and reduce cost.
Versioning ensures that any time an object is modified and uploaded to a bucket, it is saved as a new version.
Authorized users can access previous versions of objects at any time. In versioned buckets, a delete operation places a
marker on the object (without deleting prior versions). Conversely, you must use a separate operation to fully remove an
object from a versioned bucket. Use lifecycle configurations to reduce cost by automatically moving infrequently
accessed objects to lower-cost storage tiers.

Amazon EFS provides simple, scalable file storage for use with multiple concurrent Amazon EC2 instances or on-premises
systems. In stateless design, having a shared block storage system removes the risk of loss of data in situations where
one or more instances become unavailable.

# Exam Essentials

**Understand block storage vs. object storage.**

The difference between block storage and object storage is the fundamental unit of storage. With block storage, each
file saved to the drive is composed of blocks of a specific size. With object storage, each file is saved as a single
object regardless of size.

**Understand when to use Amazon Simple Storage Service and when to use Amazon Elastic Block Storage or Amazon Elastic
File System.**

This is an architectural decision based on the type of data that you are storing and the rate at which you intend to
update that data. Amazon Simple Storage Service (Amazon S3) can hold any type of data, but Amazon S3 would not be a good
choice for a database or any rapidly changing data types.

**Understand Amazon S3 versioning.**

Once Amazon S3 versioning is enabled, you cannot disable the feature—you can only suspend it. Also, when versioning is
activated, items that are deleted are assigned a delete marker and are not accessible. The deleted objects are still in
Amazon S3, and you will continue to incur charges for storing them.

**Know how to control access to Amazon S3 objects.**

IAM policies specify which actions are allowed or denied on specific AWS resources. Amazon S3 bucket policies are
attached only to Amazon S3 buckets. Amazon S3 bucket policies specify which actions are allowed or denied for principals
on the bucket to which the bucket policy is attached.

**Know how to create or select a proper primary key for an Amazon DynamoDB table.**

DynamoDB stores data as groups of attributes, known as items. Items are similar to rows or records in other database
systems. DynamoDB stores and retrieves each item based on the primary key value, which must be unique. Items are
distributed across 10 GB storage units, called partitions (physical storage internal to DynamoDB). Each table has one or
more partitions. DynamoDB uses the partition key value as an input to an internal hash function. The output from the
hash function determines the partition in which the item is stored. The hash value of its partition key determines the
location of each item. All items with the same partition key are stored together. Composite partition keys are ordered
by the sort key value. If the collection size grows bigger than 10 GB, DynamoDB splits partitions by sort key.

**Understand how to configure the read capacity units and write capacity units properly for your tables.**

When you create a table or index in DynamoDB, you must specify your capacity requirements for read and write activity.
By defining your throughput capacity in advance, DynamoDB can reserve the necessary resources to meet the read and write
activity your application requires while ensuring consistent, low-latency performance.

**Understand how to configure the read capacity units and write capacity units properly for your tables.**

When you create a table or index in DynamoDB, you must specify your capacity requirements for read and write activity.
By defining your throughput capacity in advance, DynamoDB can reserve the necessary resources to meet the read and write
activity your application requires while ensuring consistent, low-latency performance.

**Understand the use cases for DynamoDB streams.**

A DynamoDB stream is an ordered flow of information about changes to items in an DynamoDB table. When you enable a
stream on a table, DynamoDB captures information about every modification to data items in the table. Whenever an
application creates, updates, or deletes items in the table, DynamoDB Streams writes a stream record with the primary
key attributes of the items that were modified. A stream record contains information about a data modification to a
single item in a DynamoDB table. You can configure the stream so that the stream records capture additional information,
such as the before and after images of modified items.

**Know what secondary indexes are and when to use a local secondary index versus a global secondary index and the
differences between the two.**

A global secondary index is an index with a partition key and a sort key that can be different from those on the base
table.

A global secondary index is considered global because queries on the index can span all of the data in the base table,
across all partitions. A local secondary index is an index that has the same partition key as the base table, but a
different sort key. A local secondary index is local in the sense that every partition of a local secondary index is
scoped to a base table partition that has the same partition key value.

**Know the operations that can be performed using the DynamoDB API.**

now the more common DynamoDB API operations: CreateTable, UpdateTable, Query, Scan, PutItem, GetItem, UpdateItem,
DeleteItem, BatchGetItem, and BatchWriteItem. Understand the purpose of each operation and be familiar with some of the
parameters and limitations for the batch operations.

**Be familiar with handling errors when using DynamoDB.**

Understand the differences between 400 error codes and 500 error codes and how to handle both classes of errors. Also,
understand which techniques to use to mitigate the different errors. In addition, you should understand what causes a
ProvisionedThrouphputExceededException error and what you can do to resolve the issue.

**Understand how to configure your Amazon S3 bucket to serve as a static website.**

To host a static website, you configure an Amazon S3 bucket for website hosting and then upload your website content to
the bucket. This bucket must have public read access. It is intentional that everyone has read access to this bucket.
The website is then available at the AWS Region specific website endpoint of the bucket.

**Be familiar with the Amazon S3 API operations.**

Be familiar with the API operations, such as PUT, GET, SELECT, and DELETE. Understand how having versioning enabled
affects the behavior of the DELETE operation. You should also be familiar with the situations that require a multipart
upload and how to use the associated API.

**Understand the differences among the different Amazon S3 storage classes.**

The storage classes are Standard, Infrequent Access (IA), Glacier, and Reduced Redundancy. Understand the differences
and why you might choose one storage class over the other and knowing the consequences of those choices.

**Know how to use Amazon ElastiCache.**

Improve the performance of your application by deploying ElastiCache clusters as a part of your application and
offloading read requests for frequently accessed data. Use the lazy loading caching strategy in your solution to first
check the cache for your query results before checking the database.

**Understand when to choose one specific cache engine over another.**

ElastiCache provides two open source caching engines. You are responsible for choosing the engine that meets your
requirements. Use Redis when you must persist and restore your data, you need mul- tiple replicas of your data, or you
are seeking advanced features and functionality, such as sort and rank or leaderboards. Redis supports these features
natively. Alternatively, you can use Memcached when you need a simpler, in-memory object store that can be easily
partitioned and horizontally scaled.