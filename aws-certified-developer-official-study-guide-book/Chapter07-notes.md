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