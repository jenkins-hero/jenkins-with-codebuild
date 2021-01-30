This project demonstrates running Jenkins pipeline stages on AWS CodeBuild.

See accompanying article [Integrating AWS CodeBuild into Jenkins pipelines](https://tomgregory.com/integrating-aws-codebuild-into-jenkins-pipelines/)
for full step-by-step instructions.

## Pre-requisites

* Docker
* Java 11+
* AWS account with [this CloudFormation template](https://console.aws.amazon.com/cloudformation/home?region=eu-west-1#/stacks/quickcreate?templateURL=https://tomgregory-cloudformation-examples.s3-eu-west-1.amazonaws.com/codebuild-for-jenkins.yml&stackName=codebuild-for-jenkins) deployed

## Starting Jenkins

`./gradlew docker dockerRun`

Jenkins is now running on [http://localhost:8080](http://localhost:8080).

You may need to pass the Gradle property `-PawsDirectoryPath=<your .aws directory>` if you need to use a non-standard 
path to your *.aws* directory.

## Running jobs

In Jenkins click on *seed-job* then *Build Now*. 

Two new pipeline jobs will be created which run AWS CodeBuild builds in a pipeline stage:

### AWS CodeBuild example

Demonstrates CodeBuild pulling project source from GitHub. 

1. Manually trigger pipeline
1. Jenkins kicks off CodeBuild build named *github-project*
1. CodeBuild pulls project to build from GitHub and builds it
1. Jenkins pipeline continues

### AWS CodeBuild example using S3

Demonstrates CodeBuild pulling project source from S3.

1. Manually trigger pipeline
1. Jenkins uploads source to S3 bucket named *codebuild-code*
1. Jenkins kicks off CodeBuild build named *s3-project*
1. CodeBuild pulls project to build from S3 and builds it
1. Jenkins pipeline continues