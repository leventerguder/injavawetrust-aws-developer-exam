# Encryption on AWS

# Introduction to Encryption

AWS delivers a secure, scalable cloud computing platform with high availability, offering the flexibility for you to
build a wide range of applications. If you require an additional layer of security for the data you store in the AWS
Cloud, there are several options for encrypting data at rest.

# AWS Key Management Service

AWS Key Management Service (AWS KMS) is a managed AWS service that makes it easy to create and manage encryption keys to
encrypt your data across a wide range of AWS services and in your applications.

You can take advantage of a number of AWS KMS features and benefits when developing your applications. You can use AWS
KMS to make the applications and data more secure while still enabling you to innovate quickly through an API.

AWS KMS offers the following features:

- Centralized key management
- Integration with other AWS services
- Audit capabilities and high availability
- Custom key store
- Compliance

## Centralized Key Management

AWS KMS provides you with a centralized view of your encryption keys. You can create a customer master key (CMK) to
control access to your data encryption keys (data keys) and to encrypt and decrypt your data.

AWS KMS uses an Advanced Encryption Standard (AES) in 256-bit mode to encrypt and secure your data.

You can use AWS KMS to create keys in one of three ways:

- by using AWS KMS,
- by using AWS CloudHSM,
- by importing your own key material.

You can manage them with AWS KMS through the AWS Management Console or by using the AWS SDK or the AWS CLI.

AWS KMS also automatically rotates your keys once a year, without having to re-encrypt data that was previously
encrypted.

## Integration with Other AWS Services

AWS KMS provides seamless integration with other AWS services. This integration means that, as a developer, you can
quickly create keys to encrypt data that is stored in other AWS services, such as Amazon Simple Storage Service (Amazon
S3).

AWS KMS provides an AWS managed master key for a variety of AWS services that integrate with AWS KMS. You can track the
AWS managed CMKs in your account, but the service itself manages the keys.

## Auditing Capabilities and High Availability

If AWS CloudTrail is enabled for your AWS account and Region, API requests and other activity in your AWS account are
recorded to log files. With CloudTrail, you can see who has used a particular AWS KMS CMK, the API call that was sent,
and when they attempted to use that particular key.

In addition to auditing capabilities, AWS KMS is a fully managed service, which means that as your encryption needs grow
or change, AWS KMS can scale automatically to meet those needs.

The AWS CMKs do not leave the CloudHSM instances. Your keys are stored securely within the AWS Region so that no one,
including AWS employees, can retrieve your plaintext keys from AWS KMS.

## Custom Key Store

You can create your own custom key store in an CloudHSM cluster that you control, enabling you to store your AWS KMS
keys in a single-tenant environment instead of the default multi-tenant environment of AWS KMS. The use of a custom key
store incurs an additional cost for the CloudHSM cluster.

## Compliance

Achieving compliance for your applications can be a lengthy and difficult process. The security and quality controls in
AWS KMS have been validated and certified by a number of industry-specific compliance and regulatory standards.

# AWS CloudHSM

AWS CloudHSM offers third-party, validated FIPS 140-2, level-three hardware security modules in the AWS Cloud. The
hardware security module is a computing device that provides a dedicated infrastructure to support cryptographic
operations.

You can use CloudHSM to support encryption for your application while running in your own Amazon Virtual Private Cloud (
Amazon VPC).

CloudHSM provides both asymmetric and symmetric encryption capabilities.

# Controlling the Access Keys

Encryption on any system requires three components: data to encrypt, a method to encrypt the data using a cryptographic
algorithm, and the use of encryption keys with the data and the algorithm.

Managing the security of encryption keys is often performed using a key management infrastructure (KMI).
A KMI is composed of two subcomponents: the storage layer that protects the plaintext keys and the management layer
that authorizes key use. A common way to protect keys in a KMI is to use a hardware security module.

An HSM is a dedicated storage and data processing device that performs cryptographic operations using keys on the
device. An HSM typically provides tamper evidence, or resistance, to protect keys from unauthorized use.

There are three different options for how you and AWS pro- vide the encryption method and the KMI:

- You control the encryption method and the entire KMI.
- You control the encryption method, AWS provides the storage component of the KMI, and you provide the management layer
  of the KMI.
- AWS controls the encryption method and the entire KMI.

## Option 1: You Control the Encryption Method and the Entire KMI

In this option, you use your own KMI to generate, store, and manage access to keys in addition to controlling all the
encryption methods in your applications.

You are responsible for the proper storage, management, and use of keys to ensure the confidentiality, integrity, and
availability of your data.

### Amazon Simple Storage Service

You can encrypt data by using any encryption method you want and then upload the encrypted data using the Amazon Simple
Storage Service (Amazon S3) API.

AWS provides an alternative to these open source encryption tools with the Amazon S3 encryption client, which is an open
source set of APIs embedded in the AWS SDKs.

### Amazon Elastic Block Store

Amazon Elastic Block Store (Amazon EBS) provides block-level storage volumes for use with Amazon EC2 instances. Amazon
EBS volumes are network-attached and persist independently from the life of an instance.

**System-level or block-level encryption**

Amazon EBS volumes are presented to an instance as a block device, you can leverage most standard encryption tools for
file system-level or block-level encryption.

Some common block-level open source encryption solutions for Linux are Loop-AES, dm-crypt (with or without LUKS
extension), and TrueCrypt.

**File-system encryption**

You can use file system-level encryption, which works by stacking an encrypted file system on top of an existing file
system. This method is typically used to encrypt a specific directory. eCryptfs and EncFs are two Linux-based open
source examples of file system-level encryption tools.

### AWS Storage Gateway

AWS Storage Gateway is a service connecting an on-premises software appliance with Amazon S3.
You can encrypt source data on the disk volumes by using any of the file encryption methods described previously, such
as Bouncy Castle or OpenSSL, before it is written to the disk.

### Amazon Relational Database Service

technology, you must consider how you want data queries to work. Because Amazon RDS does not expose the attached disk it
uses for data storage, transparent disk encryption using techniques described in the previous.

### Amazon EMR

Amazon EMR provides an easy-to-use Hadoop implementation running on Amazon EC2.

Performing encryption throughout the Hadoop operation involves encryption and key man- agement at the following distinct
phases:

- Source data
- Hadoop Distributed File System (HDFS)
- Shuffle Phase
- Output data

If the source data is not encrypted, then this step can be skipped, and SSL can be used to help protect data in transit
to the Amazon EMR cluster. If the source data is encrypted, then your Hadoop job must decrypt the data as it is
ingested. If your job flow uses Java and the source data is in Amazon S3, you can use any of the client decryption
methods described in the previous Amazon S3 sections.

## Option 2: You Control the Encryption Method, AWS Provides the KMI Storage Component, and You Provide the KMI Management Layer

### CloudHSM

To help you decide whether CloudHSM is appropriate for your deployment, it is important to understand the role that an
HSM plays in encrypting data. You can use an HSM to generate and store key material and perform encryption and
decryption operations.

### Amazon Virtual Private Cloud

Applications must be able to access your CloudHSM appliance in an Amazon Virtual Private Cloud (Amazon VPC). The
CloudHSM client interacts with the CloudHSM appliance to encrypt data from your application. You can then send
encrypted data to any AWS service for storage.

To achieve the highest availability and durability of keys in your CloudHSM appliance, AWS recommends deploying multiple
CloudHSM applications across different Availability Zones or with an on-premises HSM appliance that you manage.

## Option 3: AWS Controls the Encryption Method and the Entire KMI

AWS provides server-side encryption of your data, transparently managing the encryption method and keys.

### AWS Key Management Service

AWS Key Management Service (AWS KMS) is a managed encryption service that lets you provision and use keys to encrypt
your data in AWS services and your applications.

Master keys in AWS KMS are used in a similar way to how master keys in an HSM are used.

AWS KMS is natively integrated with other AWS services, including Amazon EBS, Amazon S3, and Amazon Redshift, to
simplify encryption of your data within those services.

AWS SDKs are integrated with AWS KMS to enable you to encrypt data in your custom applications. For applications that
must encrypt data, AWS KMS provides global availability, low latency, and a high level of durability for your keys.

AWS KMS and other services that encrypt your data directly use a method called enve- lope encryption to balance
performance and security.

### Amazon S3

There are three ways to encrypt your data in Amazon S3 using server-side encryption.

**Server-side encryption**

You can set an API flag or use the AWS Management Console
to encrypt data before it is written to disk in Amazon S3. Each object is encrypted with
a unique data key. As an additional safeguard, this key is encrypted with a periodically rotated master key managed by
Amazon S3. Amazon S3 server-side encryption uses 256-bit Advanced Encryption Standard (AES) keys for both object and
master keys. This feature is offered at no additional cost beyond what you pay for using Amazon S3.

**Server-side encryption using customer-provided keys**

You can use your own encryption key while uploading an object to Amazon S3. Amazon S3 uses this encryption key to
encrypt your data using AES-256. After the object is encrypted, the encryption key is deleted from the Amazon S3 system
that used it to protect your data. When you retrieve this object from Amazon S3, you must provide the same encryption
key in your request. Amazon S3 verifies that the encryption key matches, decrypts the object, and returns the object to
you. This feature is offered at no additional cost beyond what you pay for using Amazon S3.

**Server-side encryption using AWS KMS**

You can encrypt your data in Amazon S3 by defining an AWS KMS master key within your account. This master key is used to
encrypt the unique object key that ultimately encrypts your object.

### Amazon EBS

When creating a volume in Amazon EBS, you can choose to encrypt it using an AWS KMS master key within your account that
encrypts the unique volume key that will ultimately encrypt your EBS volume.

### Amazon EMR

S3DistCp is an Amazon EMR feature that moves large amounts of data from Amazon S3 into HDFS, from HDFS to Amazon S3, and
between Amazon S3 buckets. With S3DistCp, you can request Amazon S3 to use server-side encryption when it writes Amazon
EMR data to an Amazon S3 bucket. This feature is offered at no additional cost beyond what you pay for using Amazon S3
to store your Amazon EMR data.

### Amazon Redshift

When creating an Amazon Redshift cluster, you can choose to encrypt all data in user-created tables. For server-side
encryption of an Amazon Redshift cluster, you can choose from the following options

**256-bit AES keys**

Data blocks (included backups) are encrypted using random 256-bit AES keys. These keys are themselves encrypted using a
random 256-bit AES database key, which is encrypted by a 256-bit AES cluster master key that is unique to your cluster.

**CloudHSM cluster master key**

The 256-bit AES cluster master key used to encrypt your database keys is generated in your CloudHSM or by using HSM
appliance on- premises. This cluster master key is then encrypted by a master key that never leaves your HSM.

**AWS KMS cluster master key**

The 256-bit AES cluster master key used to encrypt your database keys is generated in AWS KMS. This cluster master key
is then encrypted by a master key within AWS KMS. When the Amazon Redshift cluster starts up, the cluster master key is
decrypted in AWS KMS and used to decrypt the database key, which is sent to the Amazon Redshift hosts to reside only in
memory for the life of the cluster.

# Summary

If you take all responsibility for the encryption method and the KMI, you can have granular control over how your
applications encrypt data. However, that granular control comes at a cost—both in terms of deployment effort and an
inability to have AWS services tightly integrate with your applications’ encryption methods. As an alternative, you can
choose a managed service that enables easier deployment and tighter integration with AWS Cloud services. This option
offers checkbox encryption for several services that store your data, control over your own keys, secured storage for
your keys, and auditability on all data access attempts.

# Exam Essentials

**Know how to define key management infrastructure (KMI).**

A KMI consists of two infrastructure components. The first component is a storage layer that protects plaintext keys.
The second component is a management layer that authorizes use of stored keys

**Understand the available options for how you and AWS provide encryption using a KMI.**

With the first option, you control the encryption method in addition to the entire KMI. In the second option, you
control the encryption method and the management layer of the KMI, and AWS provides the storage layer. In the third
option, AWS controls the encryption method and both components of the KMI.

**Understand the maintenance trade-offs of each key management option.**

For any options that involve customers managing the components of the KMI or encryption method,maintenance increases
significantly. The increased maintenance also reduces your ability to take advantage of built-in integrations between
AWS KMS and other services.For options that involve using built-in AWS functionality, additional maintenance is required
only when migrating legacy applications to take advantage of new features.

**Understand the encryption options available in Amazon S3.**

Regardless of the key management tools and process, you are able to encrypt any objects before uploading them to an
Amazon S3 bucket. However, any custom encryption logic adds to processing overhead for the encryption and decryption of
the data. AWS provides the Amazon S3 encryption client to help streamline this process (available in the Java, Ruby, and
.NET AWS SDKs). When encrypting data on-premises, AWS has no visibility into the encryption keys or mechanisms used. For
server-side encryption, Amazon S3 supports AWS-managed keys, customer-managed keys, and encryption using AWS KMS.

**Understand the encryption options available in Amazon EBS.**

Like any on-premises block storage, Amazon EBS supports both block-level and file-system encryption. However, an
important caveat with block-level and file-system encryption tools, such as TrueCrypt and eCryptfs, is that you cannot
use them to encrypt the boot volume of an Amazon EC2 instance. Amazon EBS supports encryption by using customer-managed
keys and AWS KMS.

**Understand the encryption options available in Amazon RDS.**

Because Amazon RDS does not expose the underlying file system of databases, block-level and file-system encryp- tion
options are not available. However, standard libraries for encryption of database fields are fully supported. It is
important to evaluate the types of queries that will be run against a database before selecting an encryption process,
as this could affect the ability to run queries on encrypted data.