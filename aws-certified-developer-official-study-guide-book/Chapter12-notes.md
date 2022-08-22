# Serverless Compute

# Introduction to Serverless Compute

Serverless compute is a cloud computing execution model in which the AWS Cloud acts as the server and dynamically
manages the allocation of machine resources. AWS bases the price on the amount of resources the application consumes
rather than on prepurchased units of capacity.

# AWS Lambda

AWS Lambda is the AWS serverless compute platform that enables you to run code without provisioning or managing
servers. . With AWS Lambda, you can run code for nearly any type of application or backend service—with zero
administration.

Only upload your code, and AWS Lambda performs all the tasks you require to run and scale your code with high
availability.

AWS Lambda is sometimes referred to as a function-as-a-service (FaaS).

AWS Lambda executes code whenever the function is triggered, and no Amazon Elastic Compute Cloud (Amazon EC2) instances
need to be spun up in your infrastructure.

AWS Lambda offers several key benefits over Amazon EC2. First, there are no servers to manage. You are no longer
responsible for provisioning or managing servers, patching servers, or worrying about high availability.

Second, you do not have to concern yourself with scaling. AWS Lambda automatically scales your application by running
code in response to each trigger. Your code runs in parallel and processes each trigger individually, scaling precisely
with the size of the workload.

Third, when you run Amazon EC2 instances, you are responsible for costs associated with the instance runtime. It does
not matter whether your site receives little to no traffic— if the server is running, there are costs. With AWS Lambda,
if no one executes the function or if the function is not triggered, no charges are incurred.

With the use of AWS Lambda and other AWS services, you can begin to decouple the application, which allows you to
improve your ability to both scale horizontally and create asynchronous systems.

## Where Did the Servers Go?

Serverless computing still requires servers, but the server management and capacity planning decisions are hidden from
the developer or operator. You can use serverless code with code you deploy in traditional styles, such as
microservices. Alternatively, you can write applications to be purely serverless with no provisioned servers.

AWS Lambda uses containerization to run your code. When your function is triggered, it creates a container. Then your
code executes and returns your application or services the result. If a container is created on the first invocation,
AWS refers to this as a cold start.

Once the container starts to run, it remains active for several minutes before it terminates. If an invocation runs on a
container that is already available, that invocation runs on a warm container.

By default, AWS Lambda runs containers inside the AWS environment, and not within your personal AWS account. However,
you can also run AWS Lambda inside your Amazon Virtual Private Cloud (Amazon VPC).

# AWS Lambda Functions

This section discusses how to use AWS Lambda to execute functions, such as how to create, secure, trigger, debug,
monitor, improve, and test AWS Lambda functions.

## Creating an AWS Lambda Function

You can use any of the following methods to access AWS services and create an AWS Lambda function that will call an AWS
service:

- AWS Management Console
- AWS CLI
- AWS SDK
- AWS application programming interface (API)

When you create an AWS Lambda function, there are three options:

- Author from scratch ; Manually create all settings and options.
- Blueprints : Select a preconfigured template that you can modify.
- Serverless application repository : Deploy a publicly shared application with the AWS Serverless Application Model (
  AWS SAM)

## Execution Methods/Invocation Models

- Nonstreaming Event Source (Push Model)—Amazon Echo, Amazon Simple Storage Service (Amazon S3), Amazon Simple
  Notification Service (Amazon SNS), and Amazon Cognito.
- Streaming Event Source (Pull Model)—Amazon Kinesis or Amazon DynamoDB stream

Additionally, you can execute an AWS Lambda function synchronously or asynchronously.

## Securing AWS Lambda Functions

AWS Lambda functions include two types of permissions.

Execution permissions enable the AWS Lambda function to access other AWS resources in your account. For example, if the
AWS Lambda function needs access to Amazon S3 objects, you grant permissions through an AWS IAM role that AWS Lambda
refers to as an execution role.

Invocation permissions are the permissions that an event source needs to communicate with your AWS Lambda function.
Depending on the invocation model (push or pull), you can either update the access policy you associate with your AWS
Lambda function (push) or update the execution role (pull).

# Inside the AWS Lambda Function

The primary purpose of AWS Lambda is to execute your code. You can use any libraries, artifacts, or compiled native
binaries that execute on top of the runtime environment as part of your function code package.

## Function Package

Two parts of the AWS Lambda function are considered critical: the function package
and the function handler. The function code package contains everything you need to be available locally when your
function is executed. At minimum, it contains your code for the function itself, but it may also contain other assets or
files that your code references upon execution.

# Invoking AWS Lambda Functions

There are many ways to invoke an AWS Lambda function. You can use the push or pull method, use a custom application, or
use a schedule and event to run an AWS Lambda trigger. AWS Lambda supports the following AWS services as event sources:

- Amazon S3 , Amazon DynamoDB, Amazon Kinsesis Data Streams, Amazon SNS , Amazon Simple Email Service, Amazon Cognito
- AWS CloudFormation , Amazon CloudWatch Logs , Amazon CloudWatch Events...

# Monitoring AWS Lambda Functions

With AWS Lambda, there are two primary tools to monitor functions to ensure that they are running correctly and
efficiently: Amazon CloudWatch and AWS X-Ray.

## Using Amazon CloudWatch

Amazon CloudWatch monitors AWS Lambda functions. By default, AWS Lambda enables these metrics: invocation count,
invocation duration, invocation errors, throttled invocations, iterator age, and DLQ errors.

## Using AWS X-Ray

AWS X-Ray is a service that collects data about requests that your application serves,
and it provides tools to view, filter, and gain insights into that data to identify issues and opportunities for
optimization. For any traced request to the application, information displays about the request and response, but also
about calls that the application makes to downstream AWS resources, microservices, databases, and HTTP web APIs.

There are three main parts to the X-Ray service:

- Application code runs and uses the AWS X-Ray SDK
- AWS X-Ray daemon
- AWS X-Ray displays in the AWS Management Console.

# Summary

In this chapter, you learned about serverless compute, explored what it means to use a serverless service, and took an
in-depth look at AWS Lambda. With AWS Lambda, you learned how to create a Lambda function with the AWS Management
Console and AWS CLI and how to scale Lambda functions by specifying appropriate memory allocation settings and properly
defining timeout values. Additionally, you took a closer look at the Lambda function handler, the event object, and the
context object to use data from an event source with AWS Lambda. Finally, you looked at how to invoke Lambda functions
by using both the push and pull models and monitor functions. We wrapped up the chapter with a brief look at Amazon
CloudWatch and AWS X-Ray.

# Exam Essentials

**Know how to use execution context for reuse.**

Take advantage of execution context reuse to improve the performance of your AWS Lambda function. Verify that any
externalized configuration or dependencies that your code retrieves are stored and referenced locally after initial
execution.Limit the re-initialization of variables or objects on every invocation. Instead, use static
initialization/constructor, global/static variables, and singletons. Keep connections (HTTP or database) active, and
reuse any that were established during a previous invocation.

**Know how to use environmental variables.**

Use environment variables to pass operational parameters to your AWS Lambda function. For example, if you are writing
to an Amazon S3 bucket, instead of hardcoding the bucket name to which you are writing, configure the bucket name as an
environment variable.

**Know how to control the dependencies in your function’s deployment package.**

The AWS Lambda execution environment contains libraries, such as the AWS SDK, for the Node.js and Python runtimes. To
enable the latest set of features and security updates, AWS Lambda periodically updates these libraries. These updates
may introduce subtle changes to the behavior of your AWS Lambda function. Package all your dependencies with your
deployment package to have full control of the dependencies that your function uses.

**Know how to minimize your deployment package size to its runtime necessities.**

Minimizing your deployment package size reduces the amount of time that it takes for your deployment package to download
and unpack ahead of invocation.

**Know how memory works.**

Performing AWS Lambda function tests is a crucial step to ensure that you choose the optimum memory size configuration.
Any increase in memory size triggers an equivalent increase in CPU that is available to your function. The memory usage
for your function is determined per invocation, and it displays in the Amazon CloudWatch Logs.

**Know how to load test your AWS Lambda function to determine an optimum timeout value.**

It is essential to analyze how long your function runs to determine any problems with a dependency service. Dependency
services may increase the concurrency of the function beyond what you expect. This is especially important when your AWS
Lambda function makes network calls to resources that may not handle AWS Lambda’s scaling.

**Know how permissions for IAM policies work.**

Use the most-restrictive permissions when you set AWS IAM policies. Understand the resources and operations that your
AWS Lambda function needs, and limit the execution role to these permissions.

**Know how to use AWS Lambda metrics and Amazon CloudWatch alarms.**

Use AWS Lambda metrics and Amazon CloudWatch alarms (instead of creating or updating a metric from within your AWS
Lambda function code). This is a much more efficient way to track the health of your AWS Lambda functions, and it allows
you to catch issues early in the development process. For instance, you can configure an alarm based on the expected
duration of your AWS Lambda function execution time to address any bottlenecks or latencies attributable to your
function code.

**Know how to capture application errors.**

Leverage your log library and AWS Lambda metrics and dimensions to catch application errors, such as ERR, ERROR, and
WARNING.

**Know how to create and use dead letter queues (DLQs).**

Create and use DLQs to address and replay asynchronous function errors.
