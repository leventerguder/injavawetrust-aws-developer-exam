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