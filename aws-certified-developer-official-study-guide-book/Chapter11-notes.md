# Introduction to Refactor to Microservices

Microservices architecture is a method to design and build software applications as a suite of modular services, each
performing a specific functional task, which deploy and access application components via well-defined standard
application programming interfaces (APIs).

Containers are software-defined execution environments that you can rapidly provision and independently deploy in server
and serverless environments.

To refactor to microservices is to separate the application components into separate microservices so that each
microservice has its own data store, scales independently, and deploys on its own infrastructure.

To refactor to microservices requires a message infrastructure so that the microservices can communicate with each
other. Message queues communicate between applications.

# Amazon Simple Queue Service

Message-oriented middleware (MoM) supports messaging types in which the messages that are produced (producers) can
broadcast and publish to multiple message consumers, also known as message subscribers.

Amazon Simple Queue Service (Amazon SQS) is a fully managed message queuing service that makes it easy to decouple and
scale microservices, distributed systems, and serverless applications to assist in event-driven solutions.

Amazon SQS both moves data between distributed application components and helps you to decouple these components. Amazon
SQS is the best option for cloud-designed applications that need unlimited scalability, capacity, throughput, and high
availability.

Amazon SQS temporarily stores messages from a message producer while they wait for a message consumer to process the
message.

![](Amazon-Simple-Queue-Service-flow.png)

The producer is the component that sends the message. The consumer is the component that pulls the message off the
queue. The queue passively stores messages and does not notify you of new messages.

With Amazon SQS, multiple producers can write messages, and multiple consumers can process the messages. One of the
consumers processes each message, and when a consumer processes a message, they remove it from the queue.

## Use Amazon SQS Queue to Alleviate Log Server Failures

If you replace the log server with an Amazon SQS queue with multiple log servers, you can remove this point of failure.

There are several benefits to using the Amazon SQS queue:

- If you need to take a sign-in server offline for maintenance, the service does not interrupt. The messages remain in
  the queue until the sign-in server comes back online.
- If the number of messages grows, you can scale your sign-in service and add more servers.
- Amazon SQS automatically scales to handle an increase in incoming messages.
- Messages remain in order and deliver only one message.
- Messages can be sent to the dead-letter queue.
- Messages have a visibility timeout, a message retention period, and a receive-message wait time.
- Messages can have a long polling interval or a short polling interval (default).

The Amazon SQS is a distributed cluster of servers. There is no limit on the number of producers that can write to the
queue, and there is no limit on the number of messages that the queue can store.

## Amazon SQS Parameters

An Amazon SQS message has three basic states:

- Sent to a queue by a producer
- Received from the queue by a consumer
- Deleted from the queue

## Dead-Letter Queue

Amazon SQS supports dead-letter queues, which other queues (source queues) can target for messages that cannot process (
be consumed) successfully. Dead-letter queues are useful when you debug your application or message system because the
queues let you isolate problematic messages to determine why their process did not succeed.

Sometimes messages do not process because of a variety of possible issues, such as erroneous conditions within the
producer or consumer application or an unexpected state change that causes an issue with your application code.

AWS recommends that you set the retention period of a dead-letter queue to be longer than the retention period of the
original queue.

## Benefits of Dead-Letter Queues

The main task of a dead-letter queue is to handle message failure. Use a dead-letter queue to set aside and isolate
messages that cannot be processed correctly to determine why their processes failed. The dead-letter queue enables you
to do the following:

- Configure an alarm for any messages delivered to a dead-letter queue.
- Examine logs for exceptions that might have caused messages to be delivered to a dead-letter queue.
- Analyze the contents of messages delivered to a dead-letter queue to diagnose software or the producer’s or consumer’s
  hardware issues.
- Determine whether you have given your consumer sufficient time to process messages.

## Standard Queue Message Failures

Standard queues continue to process messages until the expiration of the retention period.
This ensures continuous processing of messages, which minimizes the chances of your queue being blocked by messages that
cannot process.

Amazon SQS standard queues work by using scalability and throughput. To achieve this, they trade off two qualities:

- Order is not guaranteed.
- Messages can appear twice.

## Monitoring Amazon SQS Queues Using Amazon CloudWatch

Amazon CloudWatch monitors your AWS resources and the applications you run on AWS in real time. You can use CloudWatch
to collect and track metrics, which are variables that you can measure for your resources and applications.

CloudWatch alarms send notifications or automatically make changes to the resources you monitor based on rules that you
define, for example, when a message is sent to the dead-letter queue.

If you must pass messages to other users, create an Amazon SQS queue, subscribe all the administrators to this queue,
and then configure Amazon CloudWatch Events to send a message on a daily cron schedule into the Amazon SQS queue.

CloudWatch provides a reliable, scalable, and flexible monitoring solution with no need to set up, manage, and scale
your own monitoring systems and infrastructure.

# Amazon Simple Notification Service

Amazon Simple Notification Service (Amazon SNS) is a flexible, fully managed producer/ consumer (publisher/subscriber)
messaging and mobile notifications web service that coordinates the delivery of messages to subscribing endpoints and
clients. Amazon SNS coordinates and manages the delivery or sending of messages to subscriber endpoints or clients to
assist in event-driven solutions.

Amazon SNS is based on the publish-subscribe model, and it allows the message producer to send a message to a topic
that has multiple subscribers that choose to receive the same message. The message is delivered to multiple subscribers,
which can then consume the message to trigger subsequent processes. A topic allows multiple receivers of the mes- sage
to subscribe dynamically for identical copies of the same notification.

By default, Amazon SNS offers 10 million subscriptions per topic and 100,000 topics per account. To request a higher
limit, contact AWS Support.

![](Amazon-SNS.png)

There are two types of clients in Amazon SNS: producers (publishers) and consumers (subscribers).

Producers communicate asynchronously with subscribers by producing and sending a message to a topic, which, in the
context of Amazon SNS, is a logical access point and communication channel.

Subscribers, such as web servers, email addresses, Amazon SQS queues, and AWS Lambda functions, consume or receive the
message or notification over one of the supported protocols, such as Amazon SQS, HTTPS, email, Short Message Service (
SMS), and AWS Lambda, when the consumer subscribes to the topic.

Amazon SNS supports the following endpoints:

- AWS Lambda
- Amazon SQS
- HTTP and HTTPS
- Email
- SMS
- Mobile PushRecords

## Transport Protocols

Amazon SNS supports notifications over multiple transport protocols. You can select trans- ports as part of the
subscription requests.

**HTTP, HTTPS:** Subscribers specify a URL as part of the subscription registration; notifications are delivered through
an
HTTP POST to the specified URL.

**Email, Email-JSON:** Messages are sent to registered addresses as email. Email-JSON sends notifications as a JSON
object,
while Email sends text-based email.

**Amazon SQS:** Users specify an Amazon SQS standard queue as the endpoint. Amazon SNS enqueues a notification message
to the specified queue (which subscribers can then process with Amazon SQS APIs, such as ReceiveMessage and
DeleteMessage). Amazon SQS does not support FIFO queues.

**SMS:** Messages are sent to registered phone numbers as AWS SMS text messages.

## Billing, Limits, and Restrictions

Amazon SNS includes a Free Tier, which allows you to use Amazon SNS free of charge for the first 1 million Amazon SNS
requests, and with no charges for the first 100,000 notifications over HTTP, no charges for the first 100 notifications
over SMS, and no charges for the first 1,000 notifications over email.

By default, Amazon SNS offers 10 million subscriptions per topic and 100,000 topics per account.