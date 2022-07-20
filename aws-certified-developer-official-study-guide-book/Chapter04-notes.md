# Hello, Databases

# Introduction to Databases

AWS offers a broad range of databases purposely built for your specific application use cases. You can also set up your
own database platform on the Amazon Elastic Compute Cloud (Amazon EC2). You can easily migrate your existing databases
with the AWS Database Migration Service (AWS DMS) in a cost-effective manner.

AWS Cloud offerings include the following databases:

- Managed relational databases - For transactional applications
- Nonrelational databases—For internet-scale applications
- Data warehouse databases—For analytics
- In-memory data store databases—For caching and real-time workloads
- Time-series databases—For efficiently collecting, synthesizing, and deriving insights from time-series data
- Ledger databases—For when you need a centralized, trusted authority to maintain a scalable, complete, and
  cryptographically verifiable record of transactions
- Graph databases—For building applications with highly connected data

**AWS Database Service Mapping to Database Type**

**Amazon Aurora , Relational Database**

A MySQL- and PostgreSQL-compatible relational database built for the cloud that combines the performance and
availability of traditional enterprise databases with the simplicity and cost-effectiveness of open source databases.

**Amazon Relational Database Service, Amazon RDS, Relational database**

A managed relational database for MySQL, PostgreSQL, Oracle, SQL Server, and MariaDB. Easy to set up, operate, and scale
a relational database in the cloud quickly.

**Amazon DynamoDB , NoSQL Database**

A serverless, managed NoSQL database that delivers consistent single-digit millisecond latency at any scale. Pay only
for the throughput and storage you use.

**Amazon Redshift , Data Warehouse**

A fast, fully managed, petabyte-scale data warehouse at one-tenth the cost of traditional solutions. Simple and
cost-effective solution to analyze data by using standard SQL and your existing business intelligence (BI) tools.

**Amazon ElastiCache , In-memory Data Store**

To deploy, operate, and scale an in-memory data store based on Memcached or Redis in the cloud.

**Amazon Neptune , Graph Database**

A fast, reliable, fully managed graph database to store and manage highly connected datasets.

**Amazon Document DB (with MongoDB compatibility) , Non-relational database**

A fast, scalable, highly available, and fully managed document database service that supports MongoDB workloads.

**Amazon Timestream, Time series database**

A fast, scalable, fully managed time series database service for IoT and operational applications that makes it easy to
store and analyze trillions of events per day at one-tenth the cost of relational databases.

**Amazon Quantum Ledger Database (Amazon QLDB) , Ledger Database**

A fully managed ledger database that provides a transparent, immutable, and cryptographically verifiable transaction log
owned by a central trusted authority.

**AWS Database Migration Service (AWS DMS) , Database Migration**

Help migrate your databases to AWS easily and inexpensively with minimal downtime.

![](Application-Mapping-to-AWS-Database-Service.png)

# Relational Databases

A relational database is a collection of data items with predefined relationships between them. These items are
organized as a set of tables with columns and rows. Tables store information about the objects to be represented in the
database.

## Characteristics of Relational Databases

Relational databases include four important characteristics: Structured Query Language, data integrity, transactions,
and atomic, consistent, isolated, and durable compliance.

**Structured Query Language**

Structured query language (SQL) is the primary interface that you use to communicate with relational databases.
The standard American National Standards Institute (ANSI) SQL is supported by all popular relational database engines.
Some of these engines have extensions to ANSI SQL to support functionality that is specific to that engine.

**Data Integrity**

Data integrity is the overall completeness, accuracy, and consistency of data. Relational databases use a set of
constraints to enforce data integrity in the database. These include primary keys, foreign keys, NOT NULL constraints,
unique constraint, default constraints, and check constraints.

**Transactions**

A database transaction is one or more SQL statements that execute as a sequence of operations to form a single logical
unit of work. Transactions provide an all-or-nothing proposition, meaning that the entire transaction must complete as
a single unit and be written to the database, or none of the individual components of the transaction will continue. In
relational database terminology, a transaction results in a COMMIT or a ROLLBACK. Each transaction is treated in a
coherent and reliable way, independent of other transactions.

**ACID Compliance**

All database transactions must be atomic, consistent, isolated, and durable (ACID)– compliant or be atomic, consistent,
isolated, and durable to ensure data integrity.

**Atomicity** requires that the transaction as a whole executes successfully, or if a part of the transaction
fails, then the entire transaction is invalid.

**Consistency** mandates that the data written to the database as part of the transaction must adhere to all defined
rules
and restrictions, including constraints, cascades, and triggers.

**Isolation** is critical to achieving concurrency control, and it makes sure that each transaction is independent unto
itself.

**Durability** requires that all of the changes made to the database be permanent when a transaction is successfully
completed.

## Managed vs. Unmanaged Databases

Managed database services on AWS, such as Amazon RDS, enable you to offload the administrative burdens of operating and
scaling distributed databases to AWS so that you don’t have to worry about the following tasks:

- Hardware provisioning
- Setup and configuration
- Throughput capacity planning
- Replication
- Software patching
- Cluster Scaling

AWS provides a number of database alternatives for developers. As a managed database, Amazon RDS enables you to run a
fully featured relational database while off-loading database administration. By contrast, you can run unmanaged
databases on Amazon EC2, which gives you more flexibility on the types of databases that you can deploy and configure;
however, you are responsible for the administration of the unmanaged databases.

## Amazon Relational Database Service

With Amazon Relational Database Service (Amazon RDS), you can set up, operate, and scale a relational database in the
AWS Cloud. It provides cost-efficient, resizable capacity for open-standard relational database engines. Amazon RDS is
easy to administer, and you do not need to install the database software. Amazon RDS manages time-consuming database
administration tasks, which frees you up to focus on your applications and business. For example, Amazon RDS
automatically patches the database software and backs up your database.

Amazon RDS assumes many of the difficult or tedious management tasks of a relational database:

**Procurement, configuration, and backup tasks**

**Security and availability**

![](Amazon-RDS-host-responsibilities.png)

## Relational Database Engines on Amazon RDS

Amazon RDS provides six familiar database engines: Amazon Aurora, Oracle, Microsoft SQL Server, PostgreSQL, MySQL, and
MariaDB. Because Amazon RDS is a managed ser- vice, you gain a number of benefits and features built right into the
Amazon RDS service.

- Automatic software patching
- Easy vertical scaling
- Easy storage scaling
- Read replicas
- Automatic backups
- Database snapshots
- Multi-AZ deployments
- Encryption
- IAM DB authentication
- Monitoring and metrics with Amazon CloudWatch.

### Automatic Software Patching

Periodically, Amazon RDS performs maintenance on Amazon RDS resources. Maintenance mostly involves patching the Amazon
RDS database underlying operating system (OS)or database engine version. Because this is a managed service, Amazon RDS
handles the patching for you.

### Vertical Scaling

If your database needs to handle a bigger load, you can vertically scale your Amazon RDS instance. At the time of this
writing, there are 40 available DB instance classes, which enable you to choose the number of virtual CPUs and memory
available.

### Easy Storage Scaling

Storage is a critical component for any database. Amazon RDS has the following three storage types:

**General Purpose SSD (gp2)**

This storage type is for cost-effective storage that is ideal for a broad range of workloads. Gp2 volumes deliver
single-digit millisecond latencies and the ability to burst to 3,000 IOPS for extended periods of time. The volume’s
size determines the performance of gp2 volumes.

**Provisioned IOPS (io1)**

This storage type is for input/output-intensive workloads that require low input/output (I/O) latency and consistent I/O
throughput.

**Magnetic Storage**

This storage type is designed for backward compatibility, and AWS recommends that you use General Purpose SSD or
Provisioned IOPS for any new Amazon RDS workloads.

### Read Replicas (Horizontal Scaling)

There are two ways to scale your database tier with Amazon RDS: vertical scaling and horizontal scaling. Vertical
scaling takes the primary database and increases the amount of memory and vCPUs allocated for the primary database.
Alternatively, use horizontal scaling (add another server) to your database tier to improve the performance of
applications that are read-heavy as opposed to write-heavy.

Read replicas create read-only copies of your master database, which allow you to offload any reads (or SQL SELECT
statements) to the read replica. The replication from the master database to the read replica is asynchronous. As a
result, the data queried from the read replica is not the latest data. If your application requires strongly consistent
reads, consider an alternative option.

At the time of this writing, Amazon RDS MySQL, PostgreSQL, and MariaDB support up to five read replicas, and Amazon
Aurora supports up to 15 read replicas. Microsoft SQL Server and Oracle do not support read replicas.

## Backing Up Data with Amazon RDS

Amazon RDS has two different ways of backing up data of your database instance: auto-mated backups and database
snapshots (DB snapshots).

### Automated Backups (Point-in-Time)

With Amazon RDS, automated backups offer a point-in-time recovery of your database. When enabled, Amazon RDS performs a
full daily snapshot of your data that is taken during your preferred backup window.

You can perform a restore up to the specific second, as long as it’s within your retention period. The default retention
period is seven days, but it can be a maximum of up to 35 days.

### Database Snapshots (Manual)

Unlike automated backups, database snapshots with Amazon RDS are user-initiated and enable you to back up your database
instance in a known state at any time. You can also restore to that specific snapshot at any time.

## Multi-AZ Deployments

In a Multi-AZ configuration, you have a primary and a standby DB instance. Updates to the primary database replicate
synchronously to the standby replica in a different Availability Zone.

The primary benefit of Multi-AZ is realized during certain types of planned maintenance, or in the unlikely event of a
DB instance failure or an Availability Zone failure.

Amazon RDS automatically fails over to the standby so that you can resume your workload as soon as the standby is
promoted to the primary.This means that you can reduce your downtime in the event of a failure.
Because Amazon RDS is a managed service, Amazon RDS handles the fail to the standby. When there is a DB instance
failure, Amazon RDS automatically promotes the standby to the primary—you will not interact with the standby directly.

Amazon RDS Multi-AZ configuration provides the following benefits:

- Automatic failover; no administration required.
- Increased durability in the unlikely event of component failure
- Increased availability in the unlikely event of an Availability Zone failure
- Increased availability for planned maintenance (automated backups; I/O activity is no longer suspended)

## Encryption

For encryption at rest, Amazon RDS uses the AWS Key Management Service (AWS KMS) for AES-256 encryption.
You can use a default master key or specify your own for the Amazon RDS DB instance. Encryption is one of the few
options that must be configured when the DB instance is created.
You cannot modify an Amazon RDS database to enable encryption. You can, however, create a DB snapshot and then restore
to an encrypted DB instance or cluster.

Amazon RDS supports using the Transparent Data Encryption (TDE) for Oracle and SQL Server.

For encryption in transit, Amazon RDS generates an SSL certificate for each database instance that can be used to
connect your application and the Amazon RDS instance.

## IAM DB Authentication

You can authenticate to your DB instance by using IAM. By using IAM, you can manage access to your database resources
centrally instead of storing the user credentials in each database. The IAM feature also encrypts network traffic to and
from the database by using SSL.

IAM DB authentication is supported only for MySQL and PostgreSQL.