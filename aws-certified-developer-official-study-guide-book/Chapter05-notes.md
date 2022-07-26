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