# Optimization

# Introduction to Optimization

Creating a software system is a lot like constructing a building. If the foundation is not solid, structural problems
can undermine the integrity and function of the building.The AWS Well-Architected Tool helps you understand the pros and
cons of decisions that you make while building systems on AWS.

By using the tool, you will learn architectural best practices for designing and operating reliable, secure, efficient,
and cost-effective systems in the AWS Cloud.

When architecting technology solutions, if you neglect the five pillars of operational excellence, security,
reliability, performance efficiency, and cost optimization, it can become challenging to build a system that delivers on
your expectations and requirements. Incorporating these pillars into your architecture helps you to produce stable and
efficient systems.

# Cost Optimization: Everyone’s Responsibility

All teams help manage cloud costs, and cost optimization is everyone’s responsibility. Make sure that costs are known
from beginning to end, at every level, and from executives to engineers. Ensure that project owners and budget holders
know what their upfront and ongoing costs are. Business decision makers must track costs against budgets and understand
return on investment (ROI).

Encourage everyone to track their cost optimization daily so that they can establish a habit of efficiency and see the
daily impact of their cost savings over time.

## Tagging

By tagging your AWS resources, you can assign custom metadata to instances, images, and other resources. For example,
you can categorize resources by owner, purpose, or environment, which helps you organize them and assign cost
accountability. When you apply tags to your AWS resources and activate the tags, AWS adds this information to the Cost
and Usage reports.

### Tag on Creation

You can make tagging a part of your build process and automate it with AWS management tools, such as AWS Elastic
Beanstalk and AWS OpsWorks.

### Enforce Tag Use

Using AWS Identity and Access Management (IAM) policies, you can enforce tag use to gain precise control over access to
resources, ownership, and accurate cost allocation.

# Reduce AWS Usage

Set a continuous practice to review your consumption of AWS resources, and understand the factors that contribute to
cost. Use various AWS monitoring tools to provide visibility, control, and cost optimization.

## Delete Unnecessary EBS Volumes

Stopping an Amazon Elastic Compute Cloud (Amazon EC2) instance leaves any attached Amazon Elastic Block Store (Amazon
EBS) volumes operational. You continue to incur charges for these volumes until you delete them.

## Stop Unused Instances

Stop instances used in development and production during hours when these instances are not in use and then start them
again when their capacity is needed. Assuming a 50-hour workweek, you can save 70 percent of costs by automatically
stopping dev/test/production instances during nonbusiness hours.

## Delete Idle Resources

Consider the following best practices to reduce costs associated with AWS idle resources, such as unattached Amazon EBS
volumes and unused Elastic IP addresses:

- The easiest way to reduce operational costs is to turn off instances that are no longer being used. If you find
  instances that have been idle for more than two weeks, it’s safe to stop or even terminate them.
- Terminating an instance, however, automatically deletes attached EBS volumes and requires effort to re-provision if
  the instance is needed again. If you decide to delete an EBS volume, consider storing a snapshot of the volume so that
  it can be restored later if needed.

## Update Outdated Resources

As AWS releases new services and features, it is a best practice to review your existing architectural decisions to
ensure that they remain cost effective and stay evergreen. As your requirements change, be aggressive in decommissioning
resources, components, and workloads that you no longer require.

## Delete Unused Keys

Each customer master key (CMK) that you create in AWS Key Management Service (AWS KMS), regardless of whether you use it
with KMS-generated key material or key material imported by you, incurs a cost you until you delete it. Before deleting
a CMK, you might want to know how many ciphertexts were encrypted under that key. Knowing how a CMK was used in the past
might help you decide whether you will need it in the future by using AWS CloudTrail usage logs. After you are sure that
you want to delete a CMK in AWS KMS, schedule the key deletion.

## Delete Old Snapshots

If your architecture suggests a backup policy that takes EBS volume snapshots daily or weekly, then you will quickly
accumulate snapshots. To reduce storage costs, check for “stale” snapshots—ones that are more than 30 days old—and
delete them. Deleting a snapshot has no effect on the volume. You can use the AWS Management Console or AWS Command Line
Interface (AWS CLI) for this purpose.

# Right Sizing

Right sizing is the process of matching instance types and sizes to performance and capac- ity requirements at the
lowest possible cost. To achieve cost optimization, right sizing must become an ongoing process within your
organization. Even if you right size workloads initially, performance and capacity requirements can change over time,
which can result in underused or idle resources.

## Select the Right Use Case

As you monitor current performance, identify the following usage needs and patterns so that you can take advantage of
potential right-sizing options:

**Steady State**

The load remains constant over time, making forecasting simple. Consider using Reserved Instances to gain significant
savings.

**Variable, but predictable**

The load changes on a predictable schedule. Consider using AWS Auto Scaling.

**Dev, test, production**

Development, testing, and production environments can usually be turned off outside of work hours.

**Temporary**

Temporary workloads that have flexible start times and can be interrupted are good candidates for Spot Instances instead
of On-Demand Instances.

## Select the Right Instance Family

When you launch an instance, the instance type that you specify determines the hardware of the host computer used for
your instance. Each instance type offers different compute, memory, and storage capabilities, and they are grouped in
instance families based on these capabilities. Depending on the AWS offering, you can determine the right instance
family for your infrastructure.

### Amazon Elastic Cloud Compute

Following are the different options for CPU, memory, and network resources:

- General purpose (includes A1, T2, M3, and M4 instance types)
- Compute optimized (includes the C3 and C4 instance types)
- Memory optimized (includes the X1, R3, and R4 instance types)
- Storage optimized (includes the I3 and D2 instance types)
- Accelerated computing (includes the P2, G3, and F1 instance types)

### Amazon Relational Database Service

- Standard performance (includes the M3 and M4 instance types)
- Burstable performance (includes T2 instance types)
- Memory optimized (includes the R3 and R4 instance types)

## Select the Right Instance Compatibility

- Virtualization type
- Network
- Platform

# Using Instance Reservations




