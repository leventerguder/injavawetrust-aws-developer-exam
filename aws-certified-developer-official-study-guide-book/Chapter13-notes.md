# Serverless Applications

# Introduction to Serverless Applications

In the previous chapter, you learned about AWS Lambda and how you can write functions that run in a serverless manner. A
serverless application is typically a combination of AWS Lambda and other Amazon services.

Serverless applications have the following three main benefits:

- No server management
- Flexible scaling
- Automated high availability

Without server management, you no longer have to provision or maintain servers. With AWS Lambda, you upload your code,
run it, and focus on your application updates.

With flexible scaling, you no longer have to disable Amazon Elastic Compute Cloud (Amazon EC2) instances to scale them
vertically, groups do not need to be auto-scaled, and you do not need to create Amazon CloudWatch alarms to add them to
load balancers. With AWS Lambda, you adjust the units of consumption (memory and execution time) and AWS adjusts the
rest of the instance appropriately.

# Web Server with Amazon Simple Storage Service (Presentation Tier)

Amazon Simple Storage Service (Amazon S3) can store HTML, CSS, images, and JavaScript files within an Amazon S3 bucket,
and can host the website like a traditional web server.

Though Amazon S3 hosts static websites, today many websites are dynamic applications,where you can use JavaScript to
create HTTP requests. These HTTP requests are sent to a Representational State Transfer (REST) endpoint service called
Amazon API Gateway, which allows the application to save and retrieve data dynamically.

## Amazon S3 Static Website

To create an Amazon S3 static website, you first need to create a bucket. Name the bucket something meaningful, such as
examplebucket.

The Amazon S3 bucket includes the region based on latency, cost, and regulatory requirements. Each object has a unique
key. You grant permissions at the object or bucket level.

## Configuring Web Traffic Logs

Amazon S3 allows you to log and capture information such as the number of visitors who access your website. To enable
logs, create a new Amazon S3 bucket to store your logs.

## Creating Custom Domain Name with Amazon Route 53

Amazon Route 53 is a highly available and scalable cloud Domain Name System (DNS) web service. It is designed to give
developers and businesses an extremely reliable and cost-effective way to route end users to internet applications by
translating names like www.example.com into the numeric IP addresses like 192.0.2.1 that computers use to connect to
each other.

Amazon Route 53 is fully compliant with IPv6 as well.

## Speeding Up Content Delivery with Amazon CloudFront

One way to decrease latency is to use Amazon CloudFront to move your content closer to your end users. Amazon CloudFront
has two delivery methods to deliver content.

Amazon CloudFront enables you to cache your data to minimize redundant data-retrieval operations. Amazon CloudFront
reduces the number of requests to which your origin server must respond directly. This reduces the load on your origin
server and reduces latency because more objects are served from Amazon CloudFront edge locations, which are closer to
your users.

Use Amazon CloudFront with Amazon S3 to improve your performance, decrease your application’s latency and costs, and
provide a better user experience. Amazon CloudFront is also a serverless service, and it fits well with serverless stack
services, especially when you use it in conjunction with Amazon S3.

## Dynamic Data with Amazon API Gateway (Logic or App Tier)

Amazon API Gateway is a fully managed, serverless AWS service, with no server that runs inside your environment to
define, deploy, monitor, maintain, and secure APIs at any scale.

Clients integrate with the APIs that use standard HTTPS requests. Amazon API Gateway can integrate with a
service-oriented multitier architecture with Amazon services,such as AWS Lambda and Amazon EC2.

The Amazon API Gateway integration strategy that provides access to your code includes the following:

**Control service**

Uses REST to provide access to Amazon services, such as AWS Lambda, Amazon Kinesis, Amazon S3, and Amazon DynamoDB. The
access methods include the following:

- Consoles
- CLI
- SDKs
- REST API requests and responses

**Execution service**

Uses standard HTTP protocols or language-specific SDKs to deploy API access to backend functionality.

Do not directly expose resources or the API—always use AWS edge services and the Amazon API Gateway service to
safeguard your resources and APIs.

## Endpoints

There are three types of endpoints for Amazon API Gateway.

**Regional endpoints**

Live inside the AWS Region, such as us-west-2.

**Edge optimized endpoints**

Use Amazon CloudFront, a content delivery web service with the AWS global network of edge locations as connection points
for clients, and integrate with your API.

**Private endpoints**

Can live only inside of a virtual private cloud (VPC).

## HTTP Methods

The Internet Engineering Task Force (IETF) is responsible for developing and documenting the HTTP protocol and how it
operates. Amazon API Gateway uses the HTTP protocol to process these HTTP methods.

## Authorizers

Use Amazon API Gateway to set up authorizers with Amazon Cognito user pools on an AWS Lambda function. This enables you
to secure your APIs and only allow users to whom you have granted specific access to your API.

## API Keys

With the Amazon API Gateway service, you can generate API keys to provide access to your API for external users, use
them to sell to your customer base, and use the API call apikey:create to create an API key.

## Integrating with AWS Lambda

With Amazon API Gateway, you can build RESTful APIs without the need to manage a server. Amazon API Gateway gives your
application a simple way (HTTPS requests) to leverage the innovation of AWS Lambda directly.

## Monitoring Amazon API Gateway with Amazon CloudWatch

Amazon API Gateway also integrates with Amazon CloudWatch. Amazon CloudWatch provides preconfigured metrics to help you
monitor your APIs and build both dashboards and alarms.

# User Authentication with Amazon Cognito

Amazon Cognito allows for simple and secure user sign-up, sign-in, and access control mechanisms designed to handle web
application authentication.

- Amazon Cognito user pools, which are secure and scalable user directories
- Amazon Cognito identity pools (federated identities), which offer social and enterprise identity federation
- Standards-based Web Identity Federation Authentication through Open Authorization (OAuth) 2.0, Security Assertion
  Markup Language (SAML) 2.0, and OpenID Connect (OIDC) support
- Multi-factor authentication
- Encryption for data at rest and data in transit
- Access control with AWS Identity and Access Management (IAM) integration
- Easy application integration (prebuilt user interface)

## Amazon Cognito User Pools

A user pool is a user directory in Amazon Cognito. With a user pool, your users can sign in to your web or mobile app
through Amazon Cognito. Users can also sign in through social identity providers, such as Facebook or Amazon, and
through Security Assertion Markup Language (SAML) identity providers.

User pools provide the following:

- Sign-up and sign-in services
- A built-in, customizable web user interface (UI) to sign in users
- Social sign-in with Facebook, Google, and Amazon, and sign-in with Security Asser- tion Markup Language (SAML)
  identity providers from your user pool
- User directory management and user profiles
- Security features, such as multi-factor authentication (MFA), check for compromised credentials, account takeover
  protection, and phone and email verification
- Customized workflows and user migration through AWS Lambda triggers

After successfully authenticating a user, Amazon Cognito issues JSON Web Tokens (JWT) that you can use to secure and
authorize access to your own APIs or exchange them for AWS credentials.

## User Interface Customization

An Amazon Cognito user pool includes a prebuilt user interface (UI) that you can use inside of your application to build
a user authentication flow quickly

## Amazon Cognito SDK

You can start developing for Amazon Cognito using the AWS Mobile SDK.
In addition to using the higher-level mobile and JavaScript SDKs, you can also use the lower-level APIs available via
the following AWS SDKs to integrate all Amazon Cognito functionality in your applications:
