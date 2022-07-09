# Hello, Storage

# Introduction to AWS Storage

The AWS Cloud is a reliable, scalable, and secure location for your data. Cloud storage is typically more reliable,
scalable, and secure than traditional, on-premises storage systems.

AWS offers object storage, file storage, block storage and data transfer services.

![](aws-storage-portfolio.png)

# Storage Fundamentals

- For block storage, Amazon has Amazon Elastic Block Store (Amazon EBS).
- For file storage, AWS has Amazon Elastic File System (Amazon EFS).
- For object storage, AWS has Amazon Simple Storage Services(Amazon S3) and Amazon S3 glacier.

## Velocity, Variety, and Volume

The first dimension to consider comprises the three Vs of big data: velocity, variety, and volume. These concepts are
applicable to more than big data. It is important to identify these traits for any data that you are using in your
applications.

**Velocity** is the speed at which data is being read or written, measured in reads per second (RPS) or writes per
second (WPS). The velocity can be based on batch processing, periodic, near-real-time, or real-time speeds.

**Variety** determines how structured the data is and how many different structures exist in the data. This can range
from highly structured to loosely structured, unstructured, or binary large object (BLOB) data.

**Volume** is the total size of the dataset. There are two main uses for data: developing valuable insight and storage
for later use.

## Storage Temperature

Data temperature is another useful way of looking at data to determine the right storage for your application. It helps
us understand how "lively" the data is: how much is being written or read and how soon it needs to be available.

**Hot** data is being worked on actively; that is, new ingests, updates, and transformations are actively contributing
to it.

**Warm** data is still being actively accessed, but less frequently than hot data. Often, items can be as small as in
hot
workloads but are updated and read in sets. Speed of access, while important, is not as crucial as with hot data. Warm
data is more balanced across the velocity and volume dimensions.

**Cold** data still needs to be accessed occasionally, but updates to this data are rare, so reads can tolerate higher
latency. Items tend to be large (tens of hundreds of megabytes or gigabytes). Items are often written and read
individually. High durability and low cost are essential. Cold data tends to be high-volume and low-velocity.

**Frozen** data needs to be preserved for business continuity or for archival or regulatory reasons, but it is not being
worked on actively. While new data is regularly added to this data store, existing data is never updated. Reads are
extremely infrequent (known as "write once, read never") and can tolerate very high latency. Frozen data tends to be
extremely high-volume and extremely low-velocity.

## Data Value

To optimize cost and/or performance further, segment data within each workload by value and temperature, and consider
different data storage options for different segments.

**Transient data** is often short-lived. The loss of some subset of transient data does not have significant impact on
the system as a whole.

**Reproducible data** contains a copy of useful information that is often created to improve performance or simplify
consumption, such as adding more structure or altering a structure to match consumption patterns.

**Authoritative data** is the source of truth. Losing this data will have significant business impact because it will be
difficult, or even impossible, to restore or replace it. For this data, we are willing to invest in additional
durability.

**Critical/Regulated data** is data that a business must retain at almost any cost. This data tends to be stored for
long periods of time and needs to be protected from accidental and malicious changes—not just data loss or corruption.
Therefore, in addition to durability, cost and security are equally important factors.

## One Tool Does Not Fit All

Likewise, there is no one-size-fits-all solution for data storage. Analyze your data and understand the dimensions that
we have discussed.

For the exam, know the availability, level of durability, and cost factors for each storage option and how they compare.

## Block, Object, and File Storage

### Block Storage

Some enterprise applications, like databases or enterprise resource planning systems (ERP systems), can require
dedicated, low-latency storage for each host. This is analogous to direct-attached storage (DAS) or a storage area
network (SAN). Block-based cloud storage solutions like Amazon EBS are provisioned with each Amazon Elastic Compute
Cloud (Amazon EC2) instance and offer the ultra-low latency required for high-performance workloads.

### Object Storage

Object storage solutions like Amazon S3 are ideal for building modern applications from scratch that require scale and
flexibility and can also be used to import existing data stores for analytics, backup, or archive. Cloud object storage
makes it possible to store virtually limitless amounts of data in its native format.

### File Storage

File storage solutions like Amazon EFS are ideal for use cases such as large content repositories, development
environments, media stores, or user home directories.

## AWS Shared Responsibility Model and Storage

AWS is responsible for securing the storage services. As a developer and customer, you are responsible for securing
access to and using encryption on the artifacts you create or objects you store.

It is a best practice always to use the principle of least privilege as part of your responsibility for using AWS Cloud
storage.

## Confidentiality, Integrity, Availability Model

The confidentiality, integrity, availability model (CIA model) forms the fundamentals of information security, and you
can apply the principles of the CIA model to AWS storage. Confidentiality can be equated to the privacy level of your
data. It refers to levels of your data.

Confidentiality can be equated to the privacy level of your data. It refers to levels of encryption or access policies
for your storage or individual files.

Integrity refers to whether your data is trustworthy and accurate.

Restrict permission of who can modify data and enable backup and versioning.

Availability refers to the availability of a service on AWS for storage, where an authorized party can gain reliable
access to the resource.

Restrict permission of who can delete data, enable multi-factor authentication (MFA) for Amazon S3 delete operation,
and enable backup and versioning.

![](CIA_model.png)

# AWS Block Storage Services

## Amazon Elastic Block Store

Amazon EBS presents your data to your Amazon EC2 instance as a disk volume, providing the lowest-latency access to your
data from single Amazon EC2 instances.

Each Amazon EBS volume is automatically replicated within its Availability Zone to protect your information from
component failure, offering high availability and durability.

Typical use cases for Amazon EBS ;

- Boot volumes on Amazon EC2 instances.
- Relational and NoSQL databases.
- Stream and log processing applications.
- Data warehousing applications.
- Big data analytics engines (like Hadoop/HDFS Amazon EMR)

Amazon EBS is designed to achieve the following:

- Availability of 99.999 percent
- Durability of replication within a single availability zone
- Annual failure rate (AFR) of between 0.1 and 0.2 percent

## Amazon EBS Volumes

Amazon EBS volumes persist independently from the running life of an Amazon EC2 instance. After a volume is attached to
an instance, use it like any other physical hard drive.

**Solid-state drive (SSD)** –backed volumes are optimized for transactional workloads involving frequent read/write
operations with small I/O size, where the dominant performance attribute is IOPS.

**Hard disk drive (HDD)** –backed volumes are optimized for large streaming workloads where throughput (measured in
MiB/s) is a better performance measure than IOPS.

![](EBS-volume-comparison.png)

![](EBS-volume-use-cases.png)

## Elastic Volumes

Elastic Volumes is a feature of Amazon EBS that allows you to increase capacity dynamically, tune performance, and
change the type of volume live. This can be done with no downtime or performance impact and with no changes to your
application.

## Amazon EBS Snapshots

You can protect your data by creating point-in-time snapshots of Amazon EBS volumes, which are backed up to Amazon S3
for long-term durability. The volume does not need to be attached to a running instance to take a snapshot.

Snapshots are incremental backups, meaning that only the blocks on the volume that have changed after your most recent
snapshot are saved, making this a cost-effective way to back up your block data.
For example, if you have a volume with 100 GiB of data, but only 5 GiB of data have changed since your last snapshot,
only the 5 GiB of modified data is written to Amazon S3.

## Amazon EBS Optimization

Recall that Amazon EBS volumes are network-attached and not directly attached to the host like instance stores.
On instances without support for Amazon EBS–optimized throughput, network traffic can contend with traffic between your
instance and your Amazon EBS volumes. On Amazon EBS–optimized instances, the two types of traffic are kept separate.

## Amazon EBS Encryption

For simplified data encryption, create encrypted Amazon EBS volumes with the Amazon EBS encryption feature.
All Amazon EBS volume types support encryption, and you can use encrypted Amazon EBS volumes to meet a wide range of
data-at-rest encryption requirements for regulated/audited data and applications.

Amazon EBS encryption uses 256-bit Advanced Encryption Standard (AES-256) algorithms and an Amazon-managed key
infrastructure called AWS Key Management Service (AWS KMS).

You can encrypt using an AWS KMS–generated key, or you can choose to select a customer master key (CMK) that you create
separately using AWS KMS.

You can also encrypt your files prior to placing them on the volume. Snapshots of encrypted Amazon EBS volumes are
automatically encrypted. Amazon EBS volumes that are restored from encrypted snapshots are also automatically encrypted.