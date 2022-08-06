# Introduction to AWS Code Services

## Continuous Delivery with AWS CodePipeline

You start with AWS CodePipeline to create a continuous integration/continuous deployment pipeline (CI/CD) that
integrates various sources, tests, deployments, or other components.

AWS CodePipeline implements AWS CodeCommit as a source in that it acts as the initialization point of your deployment
process.

AWS CodeBuild allows you to pull code and packages from various sources to create publishable build artifacts.

AWS CodeDeploy allows you to deploy compiled artifacts to infrastructure in your environment.

AWS CodePipeline is not limited to deploying application code; it can also be used to provision, configure, and manage
infrastructure.

![](Branch-view.png)

## Benefits of Continuous Delivery

By automating tests, they are consistently run against every change made to a code repository.

Second, developers are no longer tasked with completing steps other than checking in code changes. After the change has
been pushed to a source repository, initiation of the build/test process automatically begins.

Third, the fact that changes are tested immediately after check-in ensures that more bugs are caught earlier in the
development process.

Lastly, continuous delivery ensures that quality changes are delivered faster. This increases quality with decreased
time to market.

# Using AWS CodePipeline to Automate Deployments

AWS CodePipeline is a continuous integration and continuous delivery service for fast and reliable application and
infrastructure updates. AWS CodePipeline builds, tests, and deploys your code every time there is a code change, based
on the release process models you define.
This enables you to deliver features and updates rapidly and reliably. You can easily build an end-to-end solution with
prebuilt plugins for popular third-party services like GitHub, or you can integrate your own custom plugins into any
stage of your release process. With AWS CodePipeline, you pay only for what you use. There are no up-front fees or
long-term commitments.

## What Is AWS CodePipeline?

AWS CodePipeline is the underpinning of CI/CD processes in AWS.

AWS CodePipeline automatically detects and moves into the source stage. The code change (revision) passes to the build
stage, where changes are built into a package or product ready for deployment.

AWS CodePipeline provides a number of built-in integrations to other AWS services, such as AWS CloudFormation, AWS
CodeBuild, AWS CodeCommit, AWS CodeDeploy, Amazon Elastic Container Service (ECS), Elastic Beanstalk, AWS Lambda, AWS
OpsWorks Stacks, and Amazon Simple Storage Service (Amazon S3).

You define workflow steps through a visual editor within the AWS Management Console or via a JavaScript Object
Notation (JSON) structure for use in the AWS CLI or AWS SDKs.

AWS CodePipeline provides a dashboard where you can review real-time progress of revisions, attempt to retry failed
actions, and review version information about revisions that pass through the pipeline.

## AWS CodePipeline Concepts

**Pipeline**

A pipeline is the overall workflow that defines what transformations software changes will undergo.
You cannot change the name of a pipeline. If you would like to change the name, you must create a new pipeline.

**Revision**

A revision is the work item that passes through a pipeline. It can be a change to your source code or data stored in AWS
CodeCommit or GitHub or a change to the version of an archive in Amazon S3.

**Stage**

A stage is a group of one or more actions. Each stage must have a unique name. Should any one action in a stage fail,
the entire stage fails for this revision.

**Action**

An action defines the work to perform on the revision. You can configure pipeline actions to run in series or in
parallel. If all actions in a stage complete successfully for a revision, it passes to the next stage in the pipeline.

A pipeline must have two or more stages. The first stage includes one or more source actions only. Only the first stage
may include source actions.

Every action in the same stage must have a unique name.

**Source**

The source action defines the location where you store and update source files. Modifications to files in a source
repository or archive trigger deployments to a pipeline.

AWS CodePipeline supports these sources for your pipeline:

- Amazon S3
- AWS CodeCommit
- GitHub

A single pipeline can contain multiple source actions. If a change is detected in one of the sources, all source actions
will be invoked.

**Build**

You use a build action to define tasks such as compiling source code, running unit tests, and performing other tasks
that produce output artifacts for later use in your pipeline.

AWS CodePipeline supports the integrations for the following build actions:

- AWS CodeBuild
- CloudBees
- Jenkins
- Solano CI
- TeamCity

**Test**

You can use test actions to run various tests against source and compiled code, such as lint or syntax tests on source
code, and unit tests on compiled, running applications. AWS CodePipeline supports the following test integrations:

- AWS CodeBuild
- BlazeMeter
- Ghost Inspector
- Hewlett Packard Enterprise (HPE) StormRunner Load
- Nouvola
- Runscope

**Deploy**

The deploy action is responsible for taking compiled or prepared assets and installing them on instances, on-premises
servers, serverless functions, or deploying and updating infrastruc- ture using AWS CloudFormation templates

- AWS CloudFormation
- AWS CodeDeploy
- Amazon Elastic Container Service
- AWS Elastic Beanstalk
- OpsWork Stacks
- Xebia Labs

**Approval**

An approval action is a manual gate that controls whether a revision can proceed to the next stage in a pipeline.

Publish approval notifications ; Amazon Simple Notification Service (Amazon SNS) sends notices to one or more targets
that approval is pending.

**Invoke**

You can customize the invoke action within AWS CodePipeline if you leverage the power and flexibility of AWS Lambda.
Invoke actions execute AWS Lambda functions, which allows arbitrary code to be run as part of the pipeline execution.

- Backing up data volumes, Amazon S3 buckets, or databases
- Interacting with third-party products, such as posting messages to Slack channels
- Running through test interactions with deployed web applications, such as executing a test transaction on a shopping
  site
- Updating IAM Roles to allow permissions to newly created resources

**Artifact**

Artifacts are actions that act on a file or set of files. Artifacts can pass between actions and stages in a pipeline to
provide a final result or version of the files. For example, an artifact that passes from a build action would deploy to
Amazon EC2 during a deploy action.

**Transition**

Transitions connect stages in a pipeline and define which stages should transition to one another. When all actions in a
stage complete successfully, the revision passes to the next stage(s) in the pipeline.

**Managing Approval Actions**

You can use approvals to review changes manually before final release into production, or as a code review step.

# Using AWS CodeCommit as a Source Repository

AWS CodeCommit is a fully managed source control service that makes it easy for companies to host secure and highly
scalable private Git repositories.

AWS CodeCommit eliminates the need to operate your own source control system or worry about scaling its infrastructure.

## What Is AWS CodeCommit?

AWS CodeCommit is a cloud-based, highly available, and redundant version control service. AWS CodeCommit leverages the
Git framework, and it is fully compatible with existing tooling. There are a number of benefits to this service, such as
the following:

- Automatic encryption in-transit and at rest.
- Scaling to handle rapid release cycles and large repositories.
- Access control to the repository using IAM users, IAM roles, and IAM policies.
- Hypertext Transfer Protocol Secure (HTTPS) and Secure Shell (SSH) connectivity.

## AWS CodeCommit Concepts

**Credentials**

When you interact with AWS, you specify your AWS security credentials to verify who you are and whether you have
permission to access the resources that you request.

**HTTPS**

HTTPS connectivity to a Git-based repository requires a username and password, which pass to the repository as part of a
request. To use AWS CodeCommit with HTTPS credentials, you must first add them to an IAM user with sufficient
permissions to interact with the repository.

**SSH**

With SSH authentication, there is no need to install the AWS CLI to connect to your repository.

**Use the Credential Helper**

The previous HTTPS and SSH authentication methods both rely on additional credentials aside from IAM access/secret keys.
It is also possible to authenticate to AWS CodeCom- mit with IAM credentials and the AWS CodeCommit credential helper.

**Development Tools and Integrated Development Environment**

AWS CodeCommit integrates automatically with any development tools that support IAM credentials. Additionally, after you
set up HTTPS Git credentials, you are able to use any tools that support this authentication mechanism instead.

- AWS Cloud9
- Eclipse
- Intellij
- Visual Studio

**Repository**

A repository (repo) is the foundation of AWS CodeCommit. This is the location where you store source code files, track
revisions, and merge contributions (commits).

**Files**

A file is a piece of data that is subject to version control by AWS CodeCommit. AWS CodeCommit tracks any modifications
made to this file on a per-line level

**Pull Requests**

Pull requests are the primary vehicle on which you review and merge code changes between branches. Unlike branch
merging, pull requests allow multiple users to comment on changes before they merge with the destination branch.

**Commits**

Commits are point-in-time changes to contents of files in a repository.

**Branches**

Branches are ways to separate and organize groups of commits. This allows developers to organize work in a meaningful
fashion, separating changes into logical groups based on the feature or bug-fix being developed.

## Using AWS CodeCommit with AWS CodePipeline

You can use AWS CodeCommit as a source action in your pipeline. This allows you to utilize a highly available, redundant
version control system as the initialization point of your CI/CD pipeline.

When you select AWS CodeCommit as the source provider, you must provide a repository name and branch. If you use AWS
CodeCommit, it creates an Amazon CloudWatch Events rule and an IAM role to monitor the repository and branch for
changes.