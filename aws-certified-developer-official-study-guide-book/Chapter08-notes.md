# Infrastructure as Code

Using an infrastructure as code (IaC) model, instead of manually provisioning or using scripting languages, helps remove
the dependency on human intervention when you create and manage infrastructure over time.

You can use tools such as AWS CloudFormation to deploy infrastructure from a declarative template syntax.

AWS CloudFormation organizes resources into stacks, which you describe in the AWS Management Console, the AWS CLI, or
AWS software development kits (AWS SDKs).

# Using AWS CloudFormation to Deploy Infrastructure

AWS CloudFormation provides a common language for you to describe and provision all of the infrastructure resources in
your cloud environment.

AWS CloudFormation allows you to use a simple text file to model and provision, in an automated and secure manner, all
of the resources for your applications across all regions and accounts. This file serves as the single source of truth
for your cloud environment.

AWS CloudFormation is available at no additional charge, and you pay only for the AWS resources required to run your
applications.

## What Is AWS CloudFormation?

Before you deploy any application code, the first requirement is that infrastructure exists where you will deploy the
code. AWS CloudFormation aims to alleviate previous deployment issues with the use of a service that allows you to
describe your infrastructure with standardized JSON or YAML template syntax.

Two key benefits of AWS CloudFormation over procedural scripting or manual console actions are that your infrastructure
is now repeatable and that it is versionable.

## AWS CloudFormation Concepts

### Stacks

A stack represents a collection of resources to deploy and manage by AWS CloudFormation.

AWS CloudFormation manages all of the resources you declare in a stack when the stack updates. If you manually update
the resource outside of AWS CloudFormation, the result will be inconsistencies between the state AWS CloudFormation
expects and the actual resource state. This can cause future stack operations to fail.

### Change Sets

There may be times where you would like to see what changes will occur to resources
when you update a template, before the update occurs. Instead of submitting the update directly, you can generate a
change set. A change set is a description of the changes that will occur to a stack, should you submit the template.

### Permissions

AWS CloudFormation, unless otherwise specified, functions within the context of the IAM user or AWS role to invoke a
stack action. This means that if you submit a template that creates an Amazon EC2 instance (or instances), AWS
CloudFormation will fail unless your IAM user or AWS role has permissions to create instances.

### Template Structure

AWS CloudFormation uses specific template syntax in JSON or YAML.

    {
    "AWSTemplateFormatVersion": "2010-09-09", 
    "Description": "String Description", 
    "Metadata": { },
    "Parameters": { },
    "Mappings": { },
    "Conditions": { },
    "Transform": { },
    "Resources": { },
    "Outputs": { }
    }

**AWSTemplateFormatVersion**

AWSTemplateFormatVersion corresponds to the template version to which this template adheres. Do not confuse this with an
API version or the version of the developer’s template draft. Currently, AWS CloudFormation only supports the value "
2010-09-09", which you must provide as a literal string.

**Description**

The Description section allows you to provide a text explanation of the template’s purpose or other arbitrary
information.

**Metadata**

The Metadata section of a template allows you to provide structured details about the template. For example, you can
provide Metadata about the overall infrastructure to deploy and which sections correspond to certain environments,
functional groups, and so on.

**Parameters**

You can use Parameters to provide inputs into your template, which allows for more flex- ibility in how this template
behaves when you deploy it. Parameter values can be set either when you create the stack or when you perform updates.

**Mappings**

You can use the Mappings section of a template to create a rudimentary lookup tables that you can reference in other
sections of your template when you create the stack.

**Conditions**

You can use Conditions in AWS CloudFormation templates to determine when to create a resource or when a property of a
resource is defined (either in the Resources or Outputs section of the stack).

**Transforms**

As templates grow in size and complexity, there may be situations where you use certain components repeatedly across
multiple templates, such as common resources or mappings. Transforms allow you to simplify the template authoring
process through a powerful set of macros you use to reduce the amount of time spent in the authoring process.

**Resources**

The Resources section of an AWS CloudFormation template declares the actual AWS resources to be provisioned and their
properties. AWS CloudFormation requires this template section when you create stacks.

**Outputs**

Outputs are values that can be made available to use outside a single stack. You can refer- ence these values in a
number of different ways, such as cross-stack references, nested stacks, describe-stack API calls, or in the AWS
CloudFormation console.

## Intrinsic Functions

Situations can occur where values input into a template cannot be determined until the stack or change set actually is
created.

Multiple intrinsic functions are available to add significant power and flexibility to your templates.

### Fn::Base64

The Fn::Base64 intrinsic function converts an input string into its Base64 equivalent.

### Fn::Cidr

The Fn::Cidr intrinsic function allows you to convert an IP address block, subnet count, and size mask (optional) into
valid CIDR notation.

### Fn::FindInMap

After you create mappings in AWS CloudFormation, you use the Fn::FindInMap intrinsic function to query information
stored within the mapping table.

### Fn::GetAtt

Resources you create in AWS CloudFormation contain information that you can query in other parts of the same template.

### Fn::GetAZs

The Fn::GetAZs intrinsic function returns a list of availability zones for the account in which the stack is being
created.

### Fn::Join

AWS CloudFormation supports string concatenation with the Fn::Join intrinsic function.

### Fn::Select

Fn::Select allows you to choose an item in a list based on the zero-based index.

### Fn::Split

You can use Fn::Select to access the output list of strings and pass them to an index to select from different
substrings.

### Fn::Sub

If you need to build an input string with multiple variables determined at runtime, use the Fn::Sub function to populate
a template string with input variables from a variable map.

### Ref

You will use the Ref intrinsic function a lot within your template, especially when multiple resources have dependencies
and relationships between one another (such as if you create an AWS::EC2::VPC resource with two AWS::EC2::Subnet
resources).

## Condition Functions

Condition functions are special intrinsic functions for which you can optionally create resources or set resource
properties, depending on whether the condition evaluates to true or false.

### FN::AND

Returns true only if all contained conditions evaluate to true; otherwise, false returns.

### FN::EQUALS

Returns true if both compared values are equal; otherwise, false returns.

### FN::IF

Returns one of two values, depending on whether the specified condition evaluates to true or false.

### FN::NOT

Acts as a negation, returning the opposite of the evaluated condition.

### FN::OR

Returns true if any of the provided conditions are true. Otherwise, false returns.

## AWS CloudFormation Designer

AWS CloudFormation Designer is a web-based graphical interface used to design and deploy AWS CloudFormation templates.

## Custom Resources

AWS CloudFormation uses custom resource providers to handle the provisioning and configuration of custom resources.
Custom resource providers may be AWS Lambda functions or Amazon Simple Notification Service (Amazon SNS) topics.

## Resource Relationships

By default, AWS CloudFormation will track most dependencies between resources

## Stack Create, Update, and Delete Statuses

Whenever you perform an action on an AWS CloudFormation stack, the end result will bring the stack into one of three
possible statuses: Create, Update, and Delete. These statuses are visible in the AWS CloudFormation console, or if you
use the DescribeStacks action.

## Exports and Nested Stacks

Since AWS CloudFormation enforces limits on how large templates can grow and how many resources, outputs, and parameters
you can declare in one template, situations can arise where you will need to manage more infrastructure than a single
stack will allow.

## AWS CloudFormation Command Line Interface

AWS CloudFormation provides several utility functions apart from the standard API-based component of the AWS
CloudFormation CLI.

## AWS CloudFormation StackSets

AWS CloudFormation StackSets gives users the ability to control, provision, and manage stacks across multiple accounts.

A stack set acts as a logical container for stack information in an administrator account.
Though a stack set allows you to deploy stacks to multiple regions, the stack set itself exists in one region, and you
must manage it there.

Stack instances allow you to manage stacks in a target account.For example, if a stack set deploys to four regions in a
target account, you create four stack instances. An update to a stack set propagates to all stack instances in all
accounts and regions.

# Summary

In this chapter, you became familiar with provisioning and managing AWS infrastructure using AWS CloudFormation.
AWS CloudFormation allows you to describe an entire enterprise’s infrastructure as one or more template files,
achieving infrastructure as code (IaC) in an environment.

By leveraging AWS CloudFormation in a deployment pipeline, you can dynamically provision and update infrastructure over
time by simply committing code to a Git-based repository (AWS CodeCommit). You can use AWS CodePipeline to reliably
automate complex deployment processes.

AWS CloudFormation uses a declarative language (JSON or YAML template) to describe, model, and provision all
infrastructure resources for your applications across all regions and accounts in your cloud environment in an automated
and secure manner. This file serves as the single source of truth for your cloud environment. You pay only for the AWS
resources you require to run your applications.

The template contains the infrastructure to where AWS will deploy and configuration properties. After you deploy a
template in an account, you can redeploy it again in the same or different account and/or region.

A stack is a collection of resources that will be deployed and managed by AWS CloudFormation. When you submit a
template, the resources you configure are provisioned and then make up the stack itself. Any modifications to the
stack affect underlying resources. Stacks use the IAM user or AWS role authorizations to invoke an action. The template
only requires the Resources section.

When you create a stack, you can submit a template from a local file or via a URL that points to an object in Amazon S3.
If you submit the template as a local file, it uploads to Amazon S3 on your behalf.

Two key benefits of AWS CloudFormation are that your infrastructure is repeatable and that it is versionable.

A change set is a description of the changes that will occur to a stack should you sub- mit the template and/or
parameter updates. When you process stack updates, the template snippets you reference in any transforms pull from their
Amazon S3 locations. If a snippet updates without your knowledge, the updated snippet will import into the template. Use
a change set where there is a potential for data loss.

If values input into a template cannot be determined until the stack or change set is actually created, intrinsic
functions resolve this by adding dynamic functionality into AWS CloudFormation templates. Condition functions are
intrinsic functions to create resources or set resource properties that evaluate true or false conditions.

AWS CloudFormation Designer is a web-based graphical interface to design and deploy AWS CloudFormation templates. You
can create connections to make relationships between resources that automatically update dependencies between them.

AWS CloudFormation uses custom resource providers to handle the provisioning and configuration of custom resources with
AWS Lambda functions or Amazon SNS topics. You must provide a service token along with any optional input parameters.
The service token acts as a reference to where custom resource requests are sent. This can be an AWS Lambda function or
Amazon SNS topic. Custom resources can provide outputs back to AWS CloudFormation, which are made accessible as
properties of the custom resource.

Custom resources associated with AWS Lambda invoke functions whenever create, update, or delete actions are sent to the
resource provider. This resource type is incredibly useful to reference other AWS services and resources that may not
support AWS CloudFormation.

You can use custom resources associated with Amazon SNS for any long-running cus- tom resource tasks, such as
transcoding a large video file.

By default, AWS CloudFormation will track most dependencies between resources.
A resource can have a dependency on one or more other resources in a stack, in which case you create a resource
relationship to control the order of resource creation, updates, and deletion.

Whenever you perform an action on an AWS CloudFormation stack, the end result will bring the stack into one of several
possible statuses. These actions can complete or fail. In the case of a failed event, you can roll back the release
based on your update or deletion policies.

To update stacks, you can modify and resubmit the same template or create a change set; AWS CloudFormation will parse it
for changes (add, modify, or delete) and apply the modifications to the resources. You use the AWS CloudFormation
UpdatePolicy to determine how to respond to changes. When you delete a stack, by default all underlying stack resources
also delete. You use deletion policies to preserve resources when you delete a stack.

AWS Auto Scaling group update policies enforce the behavior that will occur when an update is performed on an AWS Auto
Scaling group. This depends on the type of change you make and whether you configure the AWS Auto Scaling scheduled
actions. You can replace the entire AWS Auto Scaling group or only instances inside it.

You use stack exports to share information between separate stacks. Or, you can manage AWS CloudFormation stacks
themselves as resources in a nested stack relationship. You can export stack output values to import them into other
stacks in the same account and region. This allows you to share data that generates in one stack out to other stacks in
your account.

You can assign a stack policy to a stack to allow or deny access to modify certain stack resources, which you can filter
by the type of update. Stack policies protect all resources by default with an implicit deny. To allow access to actions
on stack resources, you must apply explicit allow statements to the policy.

When you execute custom scripts on Amazon EC2 instances as part of your UserData, AWS CloudFormation provides several
important helper scripts. You can use these to inter- act with the stack to query metadata, notify a CreationPolicy or
WaitCondition, and process scripts when AWS CloudFormation detects metadata updates.

AWS CloudFormation StackSets give users the ability to control, provision, and manage stacks across multiple accounts
and regions.A stack set as a logical container for stack information in an administrator account. Each stack set will
contain information about stacks that you deploy to a single target account in one or more regions. Stack instances
allow you to manage stacks in a target account. An update to a stack set propagates to all stack instances in all
accounts and regions.

You can use a target account gate to perform evaluation tasks with AWS Lambda functions in the target account.

You cannot raise AWS CloudFormation template-specific limits through a support request. You can raise some limits, such
as the number of stacks per account.

AWS CloudFormation has built-in integrations with AWS CodePipeline as a deploy- ment provider. When a template revision
passes through a pipeline, AWS CloudFormation can reference input parameters, stack policies, and other configuration
data in the AWS CodePipeline deployment.

You can use change sets in a pipeline to include a manual review step to ensure that the changes you deploy are valid
and desired before they actually execute with the use of the Action Mode.

# Exam Essentials

**Understand Infrastructure as Code (IaC).**

You model infrastructure as code to automate the provisioning, maintenance, and retirement of complex infrastructure
across an organization. The declarative syntax allows you to describe the resource state you desire, instead of the
steps to create it. You can version and maintain IaC with the same development workflow as application and configuration
code.

**Understand the purpose of change sets.**

Change sets allow administrators to preview the changes that will take place when a given template deploys to the AWS
CloudFormation. This includes a description of resources that you will update or replace entirely. You create change
sets to help prevent stack updates that could accidentally result in the replacement of critical resources, such as
databases.

**Know the AWS CloudFormation permissions model.**

When you create, update, or delete stacks, AWS CloudFormation will operate with the same permissions as the IAM user or
IAM role that performs the stack action. For example, a user who deletes a stack that contains an Amazon EC2 instance
must also have the ability to terminate instances; otherwise, the stack delete fails. AWS CloudFormation also supports
service roles, which you can pass to the service when you perform stack actions. This requires that the user or role
have permissions to pass the service role to perform the stack action.

**Know the AWS CloudFormation template structure.**

You can use these AWS CloudFormation template properties: AWSTemplateFormatVersion, Description, Metadata, Parameters,
Mappings, Conditions, Transform, Resources, and Outputs. Templates only require the Resources property, and you must
define at least one resource in every template.

**Know how to use the intrinsic functions.**

It is important to understand the AWS CloudFormation templates intrinsic functions.

**Understand the purpose of AWS::CloudFormation::Init.**

the configuration tasks the cfn-init helper script will perform on instances that you create individually or as part of
AWS Auto Scaling launch configurations. This metadata key allows you to define a more declarative syntax for
configuration tasks compared to using procedural steps in the UserData property.

**Know the use cases for both custom resource types.**

ou can implement custom resources with AWS Lambda functions or Amazon SNS topics. The primary difference between each
type is that AWS Lambda-backed custom resources have a maximum execution duration of 5 minutes. This may not work for
custom resources that take a long time to provision or update. In those cases, Amazon SNS topics backed by Amazon EC2
instances would allow for long running tasks.

**Understand how AWS CloudFormation manages resource relationships.**

AWS CloudFormation will automatically reorder resource provisioning and update steps based on known dependencies. For
example, if a template declares an Amazon VPC and a subnet, the subnet will not create before the Amazon VPC (a subnet
requires an Amazon VPC ID during creation). However, AWS CloudFormation is not aware of all possible relationships, so
you must manually declare them with the DependsOn property. If a template declares an Amazon EC2 instance and AWS
DynamoDB table, and the table is referenced inside the instance’s UserData property, you must declare a DependsOn
property that states the instance depends on the table.

**Understand wait conditions and creation policies.**

n some cases, resources in a template should wait for other resources to provision and configure before starting their
tasks. For example, you may want to prevent creation of a load balancer resource until instances in an AWS Auto Scaling
group have installed a web application. In those cases, you can use either wait conditions or creation policies. Wait
conditions require you to add two separate resources to the template (AWS::CloudFormation::WaitCondition and AWS::
CloudFormation:: WaitConditionHandle). The instance’s UserData property references the wait condition handle, where a
success or failure signal will be sent. A creation policy does not require the additional resources, and it allows for
additional options such as timeouts and signal counts.

**Understand how stack updates affect resources.**

When you update a stack, resources may behave differently when properties update. If an Amazon S3 bucket is created as
part of a stack and later the bucket policy is updated, the resource will update with no interruption. However, if the
bucket name later updates, you must replace the bucket. Resources can undergo one of three types of updates: update with
no interruption, update with some interruption, and replace update.

**Know how to use exports and nested stacks to share stacks.**

Stack exports allow you to access stack outputs in other stacks in the same region. Exports, however, come with some
limitations. For example, you cannot delete stacks that export values until all other stacks that import the exported
value have been modified to no longer include the import. Nested stacks make use for the AWS::CloudFormation::Stack
resource type. This way, a single stack can create multiple “child” stacks, which can declare their own resources (
including other stacks). This is a useful mechanism to work around some service limits such as the number of resources
per template (200).

**Understand stack policies.**

To prevent updates to critical stack resources, you implement stack policies. A stack policy declares what resources you
can and cannot update and under what circumstances. A stack containing an Amazon RDS instance, for example, can include
a stack policy that prevents updates that require replacement of the database instance.