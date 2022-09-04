# Monitoring and Troubleshooting

# Introduction to Monitoring and Troubleshooting

Monitoring the applications and services you build is vital to the success of any information technology (IT)
organization. With the AWS Cloud, you can leverage monitoring resources to drive business decisions such as what
resources to create, improve, optimize, and secure.

The AWS Cloud provides fully managed services to help you implement monitoring solutions that are reliable, scalable,
and secure. AWS offers services to help you monitor, log, and analyze your applications and infrastructure.

In this section, you explore Amazon CloudWatch, AWS CloudTrail, and AWS X-Ray.

# Amazon CloudWatch

Amazon CloudWatch is a monitoring and metrics service that provides you with a fully managed system to collect, store,
and analyze your metrics and logs. By using CloudWatch, you can create notifications on changes in your environment.

Typical use cases include the following:

- Infrastructure monitoring and troubleshooting
- Resource optimization
- Application monitoring
- Logging analytics
- Error reporting and notification

CloudWatch enables you to collect and store monitoring and operations data from logs, metrics, and events that run on
AWS and on-premises resources. To ensure that your applications run smoothly, you can use CloudWatch to perform the
following tasks:

- Set alarms
- Visualize logs and metrics
- Automate recovery from errors
- Troubleshoot issues
- Discover insights that enable you to optimize your resources

## How Amazon CloudWatch Works

CloudWatch acts as a metrics repository, storing metrics and logs from various sources. These metrics can come from AWS
resources using built-in or custom metrics.

CloudWatch can process these metrics into statistics that are made available through the CloudWatch console, AWS APIs,
the AWS Command Line Interface (AWS CLI), and AWS software development kits (AWS SDKs). Using CloudWatch, you can
display graphs, create alarms, or integrate with third-party solutions.

## Amazon CloudWatch Logs

Though most commercial standard applications already produce some form of logging, most modern applications are deployed
in distributed or service-oriented architectures. Collecting and processing these logs can be a challenge as a system
grows and expands across multiple regions. Centralized logging using CloudWatch Logs can overcome this challenge. With
CloudWatch Logs, you can set up a central log storage location to ingest and process logs at scale.

## Log Groups

A log group is collection of log streams. For example, if you have a service that consists of a cluster of multiple
machines, a log group would be a container for the logs from each of the individual instances.

## Log Streams

A log stream is a sequence of log events such as a single log file from one of your instances.

## Log Events

A log event is a record of some activity from an application, process, or service. This is analogous to a single line in
a log file.

## Amazon CloudWatch Alarms

After data points are established in CloudWatch, either as metrics or as logs (from which you generate metrics), you can
set alarms to monitor your metrics and trigger actions in response to changes in state.
CloudWatch alarms have three possible states: OK, ALARM, and INSUFFICIENT_DATA.

## Amazon CloudWatch Dashboards

CloudWatch offers a convenient way to observe operational metrics for all of your applications. CloudWatch dashboards
are customizable pages in the CloudWatch console that you can use to monitor resources in a single view.

# AWS CloudTrail

All actions in your AWS account are composed of API calls, regardless of the origin (the AWS Management Console or
programmatic/scripted actions). . As you create resources in your account, API calls are being made to AWS services in
different regions around the world. AWS CloudTrail is a fully managed service that continuously monitors and records API
calls and stores them in Amazon S3.
You can use these logs to troubleshoot and resolve operational issues, meet and verify regulatory compliance, and
monitor or alarm on specific events in your account.

CloudTrail helps answer the following five key questions about monitoring access:

- Who made the API call?
- When was the API call made?
- What was the API call?
- Which resources were acted upon in the API call?
- Where was the origin of the API call?

## AWS CloudTrail Events

A CloudTrail event is any single API activity in an AWS account. This activity can be an action triggered by any of the
following:

- AWS IAM User
- AWS IAM Role
- AWS Service

CloudTrail tracks two types of events: management events and data events. Events are recorded in the region where the
action occurred, except for global service events.

### Global Service Events

Some AWS services allow you to create, modify, and delete resources from any region. These are referred to as global
services. Examples of global services include the following:

- IAM
- AWS Security Token Service (AWS STS)
- Amazon CloudFront
- Amazon Route 53

Global services are logged as occurring in US East (N. Virginia) Region. Any trails cre- ated in the CloudTrail console
log global services by default, which are delivered to the Amazon S3 bucket for the trail.

# AWS X-Ray

The services covered so far are centered on the concept of using logs as monitoring and troubleshooting tools.
Developers often write code, test the code, and inspect the logs. If there are errors, they may add breakpoints, run the
test again, and add log statements. This works well in small cases, but it becomes cumbersome as teams, software, and
infrastructure grow. Traditional troubleshooting and debugging processes do not work well at scaling across multiple
services.

Troubleshooting cross-service and cross-region interactions can be especially difficult when different systems use
varying log formats.

## AWS X-Ray Use Cases

X-Ray helps developers build, monitor, and improve applications. Use cases include the following:

- Identifying performance bottlenecks
- Pinpointing specific service issues
- Identifying errors
- Identifying impact to users

X-Ray integrates with the AWS SDK, adding traces to track your application requests as they are generated and received
from various services.

## Tracking Application Requests

X-Ray can track a user request using a trace, segment, and subsegment.

**Trace**

A trace is the path of a request through your application. This is the end-to-end request from the client—from its entry
into your environment to the backend and back to the user. A trace ID is passed through the AWS services with the
request so that X-Ray can collate related segments.

**Segment**

A segment is data from a particular service. When a segment is reported to X-Ray, a trace ID is reported. Segments are
analogous to links in a chain whereby the chain is the request generated by the user. In the example microservice, two
segments correspond to two services: the front-end service and the backend API.

**Subsegment**

A subsegment identifies the underlying API calls made from a particular service. Subsegments are collated into segments.
In this scenario, the backend API sends requests to Amazon DynamoDB and Amazon SQS.

# Summary

AWS provides multiple options for monitoring and troubleshooting your applications. As you have discovered, AWS services
help you manage logs from various systems, either running on the cloud or on-premises, create triggers that notify you
about application health and issues in your infrastructure, and build applications with modern debugging tools for
distributed applications. These services overcome the difficulties of creating a centralized logging solution.

# Exam Essentials

**Know what Amazon CloudWatch is and why it is used.**

CloudWatch is the service used to aggregate, analyze, and alert on metrics generated by other AWS services. It is used
to monitor the resources you create in AWS and the on-premises infrastructure. You can use CloudWatch to store logs from
your applications and trigger actions in response to events.

**Know what common metrics are available for Amazon Elastic Compute Cloud (Amazon EC2) in Amazon CloudWatch.**

- CPUUtilization
- DiskReadOps
- DiskReadBytes
- DiskWriteOps
- DiskWriteBytes
- NetworkIn
- StatusCheckFailed

**Understand the difference between high-resolution and standard-resolution metrics.**

High-resolution metrics are delivered in a period of less than one minute. Standard resolution metrics are delivered in
a period greater than or equal to one minute.

**Know what AWS CloudTrail is and why it is used.**

CloudTrail is used to monitor API calls made to the AWS Cloud for various services. CloudTrail helps IT administrators,
IT security administrators, DevOps engineers, and auditors to enable compliance and the monitoring of access to AWS
resources within an account.

**Know what AWS CloudTrail tracks automatically.**

By default, CloudTrail tracks the last 90 days of activity. These events are limited to management events with create,
modify, and delete API calls.

**Understand the difference between AWS CloudTrail management and data events.**

Management events are operations performed on resources in your AWS account. Data events are operations performed on
data stored in AWS resources. Examples are creating or deleting objects in Amazon S3 and inserting or updating items in
an Amazon DynamoDB table.

**Know what AWS X-Ray is and why it is used.**

X-Ray is a service that collects data about your application requests, including the various subservices or systems that
perform tasks to complete a request. X-Ray is commonly used to help developers find bottlenecks in distributed
applications and monitor the health of various components in their services.

**Know the basics of AWS X-Ray and how it helps troubleshoot applications.**

X-Ray records requests by initiating a trace ID with the origin of the request. This trace ID is added as a header to
the request that propagates to various services. If you enable the X-Ray SDK in your applications, X-Ray submits
telemetry and the request as segments for each service and subsegments for downstream services upon which you depend.
Using these traces, X-Ray collates the data to view request performance metrics, such as latency and error rates. The
data can then be used to create a graph of your application and its dependencies and the health of any requests your
application might make.