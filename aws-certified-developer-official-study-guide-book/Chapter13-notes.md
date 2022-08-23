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

Do not directly expose resources or the API—always use AWS edge ser- vices and the Amazon API Gateway service to
safeguard your resources and APIs.


