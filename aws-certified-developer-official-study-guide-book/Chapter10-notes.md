# Introduction to Authentication and Authorization

Authentication is the process or action that verifies the identity of a user or process. Authorization is a security
mechanism that determines access levels or permissions related to system resources including files, services, computer
programs, data, and application features. The authentication and authorization process grants or denies user access to
network resources based on the identity.

AWS Identity and Access Management (IAM) allows you to create identities (users, groups, or roles) and control access to
various AWS services through the use of policies. IAM serves as an identity provider (IdP).

The following are the benefits of integrating an existing IdP:

- Users are no longer required to manage multiple sets of credentials.
- There are fewer credentials to administer.
- Credentials are centrally managed.
- It is easier to establish and enforce compliance standards.

As an IdP, AWS is responsible for storing identities and providing the mechanism for authentication. You can use AWS as
an IdP for the following:

- AWS services
- Applications running on AWS infrastructure
- Applications running on non-AWS infrastructure, such as web or mobile applications

There are multiple benefits for using AWS as the IdP. AWS provides a managed service, eliminates single points of
failure, is highly available, and can scale as needed. AWS also provides a number of tools, such as Amazon CloudWatch
and AWS CloudTrail, to manage, control, and audit this service.

Using a third party to provide identity services is known as federation.

# Different Planes of Control

There are two different planes of access used to manage and access AWS services: a control plane and a data plane.

The control plane permits access to perform operations on a particular AWS instance.

AWS can control access to this plane through various AWS application programming interface (AWS API) operations.
The data plane permits access to the application running on AWS.
The data plane permits access to sign in to the compute instance using Secure Shell (SSH) or Remote Desktop Protocol (
RDP) and to make changes to the guest operating system or to the application itself.

# Identity and Authorization

AWS establishes identity in several different ways.

![](AWS-Identity.png)

AWS establishes authorization by user-executed APIs. AWS controls operations and tasks through APIs. Policies are
JavaScript Object Notation (JSON) documents that show attribute-value pairs. Every policy document requires a minimum of
three attribute-value pairs: effect, action, and resource.

Effect has the API value of either ALLOW or DENY. The entity (whether a user, group, or role) is either granted the
permission to execute that API or denied the permission to execute that API.

Action determines whether the API is allowed or denied. Actions can be determined by an individual API, a grouping of
APIs for the same service using a wildcard (for example, S3:* includes all Amazon Simple Storage Service (Amazon S3
APIs), or APIs for different services.

Resource determines where the API is being allowed or denied. For example, with Amazon S3, you can allow the execution
of an API in a particular bucket, object, or particular group of objects (using the wildcard *).

## Federation Defined

A federation consists of two components: identity provider and identity consumer.

Each component plays a different role in the process of federation.An identity provider
stores identities, provides a mechanism for authentication, and provides a course level of authorization. An identity
consumer stores a reference to the identity, providing authorization at a greater granularity than the identity
provider.

## Federation with AWS

Federation with AWS allows for two things. First, it allows you to use AWS as an IdP to gain access to both AWS and
non-AWS resources.

Amazon Cognito is an AWS service that acts as an IdP.

Second, you can use non-AWS resources like Security Assertion Markup Language (SAML) 2.0, OpenID Connect (OIDC), or
Microsoft Active Directory as the IdP to facilitate single sign-on (SSO).

## Custom Build an Identity Provider

Custom builds were the original method of federation within AWS, but they have since been supplanted by SAML, OIDC, and
Microsoft Active Directory.

## Cross-Account Access

When you need to access resources across multiple AWS accounts, cross-account access enables you to do so by using only
one set of credentials. You can grant users access to resources in company accounts without having to maintain multiple
user entities, and your users do not have to remember multiple passwords.

## Security Assertion Markup Language

Security Assertion Markup Language (SAML) provides federation between an IdP and a service provider (SP) when you are in
an AWS account and a trust relationship has been established between the IdP and the SP.

You interact only with the IdP, and all authentication and authorization occurs between you and the IdP.

## OpenID Connect

OpenID Connect (OIDC) is the successor to SAML. OIDC is easier to configure than SAML and uses tokens rather than
assertions to provide access. Most use cases for OIDC involve external versus internal users.

## Microsoft Active Directory

Microsoft Active Directory is the identity provider for a majority of corporations. You use the Active Directory forest
trusts to establish trust between an Active Directory domain controller and AWS Directory Service for Microsoft Active
Directory (AWS Managed Microsoft AD).

## AWS Single Sign-On

AWS Single Sign-On (AWS SSO) is an AWS service that manages SSO access. AWS SSO allows users to sign in to a user portal
with their existing corporate credentials and access both AWS accounts and business accounts. You can have multiple
permission sets, allowing for greater granularity and control over access.

## AWS CLI Access

You can sign in to the AWS SSO user portal with your existing corporate credentials and receive all AWS CLI credentials
for your AWS accounts from a central location.

## Management with AWS Organizations

AWS SSO enables management of SSO access and user permissions for your AWS accounts managed through AWS Organizations.
Additional setup in the individual accounts is not required.

## Integration with Microsoft Active Directory

AWS SSO integrates with Microsoft Active Directory through the Directory Service, enabling you to sign in to the user
portal using your Active Directory credentials.