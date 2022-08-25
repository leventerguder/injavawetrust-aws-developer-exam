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

# Amazon Aurora Serverless

Amazon Aurora Serverless is an on-demand, auto-scaling configuration for the Aurora MySQL-compatible edition, where the
database automatically starts, shuts down, and scales up or down as needed by your application.

This allows you to run a traditional SQL database in the cloud without needing to manage any infrastructure or
instances.

With Amazon Aurora Serverless, you also get the same high availability as traditional Amazon Aurora, which means that
you get six-way replication across three Availability Zones inside of a region in order to prevent against data loss.

Amazon Aurora Serverless is great for infrequently used applications, new applications, variable workloads,
unpredictable workloads, development and test databases, and multitenant applications. This is because you can scale
automatically when you need to and scale down when application demand is not high. This can help cut costs and save you
the heartache of managing your own database infrastructure.

Amazon Aurora Serverless gives you many of the similar benefits as other serverless technologies, such as AWS Lambda,
but from a database perspective. Managing databases is hard work, and with Amazon Aurora Serverless, you can utilize a
database that automatically scales and you don’t have to manage any of the underlying infrastructure.

# AWS Serverless Application Model

The AWS Serverless Application Model (AWS SAM) allows you to create and manage resources in your serverless
application with AWS CloudFormation to define your serverless application infrastructure as a SAM template.

A SAM template is a JSON or YAML configuration file that describes the AWS Lambda functions, API endpoints, tables, and
other resources in your application.

With simple commands, you upload this template to AWS CloudFormation, which creates the individual resources and groups
them into an AWS CloudFormation stack for ease of management. When you update your AWS SAM template, you re-deploy the
changes to this stack. AWS CloudFormation updates the individual resources for you.

AWS SAM is an extension of AWS CloudFormation. You can define resources by using the AWS CloudFormation in your AWS SAM
template.

To summarize, AWS SAM allows you to provision serverless resources more rapidly with less code by extending AWS
CloudFormation.

# AWS SAM CLI

Now that we’ve addressed AWS SAM, let’s take a closer look at the AWS SAM CLI. With AWS SAM, you can define templates,
in JSON or YAML, which are designed for provisioning serverless applications through AWS CloudFormation.

AWS SAM CLI is a command line interface tool that creates an environment in which you can develop, test, and analyze
your serverless-based application, all locally.

AWS SAM CLI also allows you to develop and test your code quickly, and this gives you the ability to test it locally,
which allows you to develop it faster. Previously, you would have had to upload your code each time you wanted to test
an AWS Lambda function. Now, with the AWS SAM CLI, you can develop faster and get your application out the door more
quickly.

# AWS Serverless Application Repository

The AWS Serverless Application Repository enables you to deploy code samples, components, and complete applications
quickly for common use cases, such as web and mobile backends, event and data processing, logging, monitoring, Internet
of Things (IoT), and more. Each application is packaged with an AWS SAM template that defines the AWS resources.
Publicly shared applications also include a link to the application’s source code. There is no additional charge to use
the serverless application repository. You pay only for the AWS resources you use in the applications you deploy.

You can also use the serverless application repository to publish your own applications and share them within your team,
across your organization, or with the community at large. This allows you to see what other people and organizations are
developing.

# Summary

This chapter covered the AWS serverless core services, how to store your static files inside of Amazon S3, how to use
Amazon CloudFront in conjunction with Amazon S3, how to integrate your application with user authentication flows using
Amazon Cognito, and how to deploy and scale your API quickly and automatically with Amazon API Gateway.

Serverless applications have three main benefits: no server management, flexible scaling, and automated high
availability. Without server management, you no longer have to provision or maintain servers. With AWS Lambda, you
upload your code, run it, and focus on your application updates. With flexible scaling, you no longer have to disable
Amazon EC2 instances to scale them vertically, groups do not need to be auto-scaled, and you do not need to create
Amazon CloudWatch alarms to add them to load balancers. With AWS Lambda, you adjust the units of consumption (memory and
execution time), and AWS adjusts the rest of the instance appropriately. Finally, serverless applications have built-in
availability and fault tolerance. When periods of low traffic occur, you do not spend money on Amazon EC2 instances that
do not run at their full capacity.

You can use an Amazon S3 web server to create your presentation tier. Within an Amazon S3 bucket, you can store HTML,
CSS, and JavaScript files. JavaScript can create HTTP requests. These HTTP requests are sent to a REST endpoint service
called Amazon API Gateway, which allows the application to save and retrieve data dynamically by triggering a Lambda
function.

After you create your Amazon S3 bucket, you configure it to use static website hosting in the AWS Management Console and
enter an endpoint that reflects your AWS Region.

Amazon S3 allows you to configure web traffic logs to capture information, such as the number of visitors who access
your website in the Amazon S3 bucket.

One way to decrease latency and improve your performance is to use Amazon CloudFront with Amazon S3 to move your content
closer to your end users. Amazon CloudFront is a serverless service.

The Amazon API Gateway is a fully managed service designed to define, deploy, and maintain APIs. Clients integrate with
the APIs using standard HTTPS requests. Amazon API Gateway can integrate with a service-oriented multitier architecture.
The Amazon API Gateway provides dynamic data in the logic or app tier.

There are three types of endpoints for Amazon API Gateway: regional endpoints, edge-optimized endpoints, and private
endpoints.

In the Amazon API Gateway service, you expose addressable resources as a tree of API Resources entities, with the root
resource (/) at the top of the hierarchy. The root resource is relative to the API’s base URL, which consists of the API
endpoint and a stage name.

You use Amazon API Gateways to help drive down the total response-time latency of your API. Amazon API Gateway uses the
HTTP protocol to process these HTTP methods and send/receive data to and from the backend. Serverless data is sent to
AWS Lambda to process.

You can use Amazon Route 53 to create a more user-friendly domain name instead of using the default host name (Amazon S3
endpoint). To support two subdomains, you create two Amazon S3 buckets that match your domain name and subdomain.

A stage is a named reference to a deployment, which is a snapshot of the API. Use a
stage to manage and optimize a particular deployment. You create stages for each of your environments such as DEV, TEST,
and PROD, so you can develop and update your API and applications without affecting production. Use Amazon API Gateway
to set up authorizers with Amazon Cognito user pools on an AWS Lambda function. This enables you to secure your APIs.

An Amazon Cognito user pool includes a prebuilt user interface (UI) that you can use inside your application to build a
user authentication flow quickly. A user pool is a user directory in Amazon Cognito. With a user pool, your users can
sign in to your web or mobile app through Amazon Cognito. Users can also sign in through social identity providers
such as Facebook or Amazon and through Security Assertion Markup Language (SAML) identity providers.

Amazon Cognito identity pools allow you to create unique identities and assign permissions for your users to help you
integrate with authentication providers. With the combination of user pools and identity pools, you can create a
serverless user authentication system.

You can choose how users sign in with a username, an email address, and/or a phone number and to select attributes.
Attributes are properties that you want to store about your end users. You can also configure password policies.
Multi-factor authentication (MFA) prevents anyone from signing in to a system without authenticating through two
different sources, such as a password and a mobile device–generated token. You create an Amazon Cognito role to send
Short Message Service (SMS) messages to users.

The AWS Serverless Application Model (AWS SAM) allows you to create and manage resources in your serverless application
with AWS CloudFormation as a SAM template.
A SAM template is a JSON or YAML file that describes the AWS Lambda function, API endpoints, and other resources. You
upload the template to AWS CloudFormation to create a stack. When you update your AWS SAM template, you redeploy the
changes to this stack, and AWS CloudFormation updates the resources. You can use AWS SAM to create a template of your
serverless infrastructure, which you can then build into a DevOps pipeline.

The AWS Serverless Application Repository enables you to deploy code samples, components, and complete applications
for common use cases. Each application is packaged with an AWS SAM template that defines the AWS resources.

Additionally, you learned the differences between the standard three-tier web applica- tions and the AWS serverless
stack. You learned how to build your infrastructure quickly with AWS SAM and AWS SAM CLI for testing and development
purposes.

# Exam Essentials

**Know serverless applications’ three main benefits.**

The benefits are as follows:

- No server management
- Flexible scaling
- Automated high availability

**Know what no server management means**

Without server management, you no longer have to provision or maintain servers. With AWS Lambda, you upload your code,
run it, and focus on your application updates.

**Know what flexible scaling means.**

With flexible scaling, you no longer have to disable Amazon Elastic Compute Cloud (Amazon EC2) instances to scale them
vertically, groups do not need to be auto-scaled, and you do not need to create Amazon CloudWatch alarms to add them
to load balancers. With AWS Lambda, you adjust the units of consumption (memory and execution time), and AWS adjusts the
rest of the instances appropriately.

**Know what serverless applications mean.**

Serverless applications have built-in availability and fault tolerance. You do not need to architect for these
capabilities, as the services that run the application provide them by default. Additionally, when periods of low
traffic occur on the web application, you do not spend money on Amazon EC2 instances that do not run at their full
capacity.

**Know what services are serverless.**

On the exam, it is important to understand which Ama- zon services are serverless and which ones are not. The following
services are serverless:

- Amazon API Gateway
- AWS Lambda
- Amazon SQS
- Amazon SNS
- Amazon Kinesis
- Amazon Cognito
- Amazon Aurora Serverless
- Amazon S3

**Know how to host a serverless web application.**

Hosting a serverless application means that you need Amazon S3 to host your static website, which comprises your HTML,
JavaScript, and CSS files.

For your database infrastructure, you can use Amazon DynamoDB or Amazon Aurora Serverless.

For your business logic tier, you can use AWS Lambda.

For DNS services, you can utilize Amazon Route 53.

If you need the ability to host an API, you can use Amazon API Gateway.

Finally, if you need to decrease latency to portions of your application, you can utilize services like Amazon
CloudFront, which allows you to host your content at the edge.