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