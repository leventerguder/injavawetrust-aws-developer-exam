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
