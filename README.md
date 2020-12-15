## AWS Security Demo

This demo shows you two different approaches to automating security compliance controls at AWS. This automation is real time and is event driven. This means it reacts to events happening in your AWS account and makes sure none of them violate any security policies or constraints. This is a strong, shining example of how to easily automate security into the DevSecOps model, thus boosting business velocity and maximizing successful outcomes on your projects.

### Objectives

#### What you will learn

* Using [AWS Config](https://aws.amazon.com/config) to define a set of security rules and track resource compliance
* Deploying required resources to power security automation using [AWS CloudFormation](https://aws.amazon.com/cloudformation/)
* Enabling automated remediation of certain rules that support it
* Interacting with the AWS APIs using the [aws-cli](https://aws.amazon.com/cli/) to create an S3 bucket for testing purposes.
* Deploying an open source tool using [Terraform](https://www.terraform.io/) that is a competitor to AWS Config
  * Seeing how it is faster, cheaper, and more configurable

#### Take aways

* Brainstorm ideas on how you could leverage similar security automation concepts on your project(s)
* Ask around and see if similar automation already exists.
  * If it does - see if you have any ideas on how to improve it
  * If not - come up with a plan and pitch it

#### How the demo will work

For the first demo, we will use AWS CloudFormation to automate the deployment of the required resources to deploy an AWS Config rule to monitor for [S3 buckets](https://aws.amazon.com/s3/) that do not have access logging configured. Once detected, this rule will also automatically remediate non-compliant resources by configure access logging with a preconfigured bucket. Additionally, [SNS](https://aws.amazon.com/sns/) will send an email notification at each step of the process.

For the second demo, we will use Terraform to automate the deployment of an open source tool called [Reflex](https://reflexivesecurity.com/). It leverages [AWS EventBridge](https://aws.amazon.com/eventbridge/) and a collection of python [Lambdas](https://aws.amazon.com/lambda/) to mimic what AWS Config does. The biggest wins with this tool are that it detects and responds faster, is significantly cheaper, and you can create any rule you want with Python code.

#### Wrap Up Assessement

1. Which of the two approaches in this demo more closely matches or is more compatible with your project(s) architecture?
2. What are some of the advantages and disadvantages of each approach?
3. What are some other things that we could find or create a rule for to make an AWS account more secure that wasn't covered in this demo?

### Prerequisites

* Install the [aws-cli](https://aws.amazon.com/cli/). Please reach out to Jesse Adams if you would like access to the Acuity Labs AWS account.
* Have an AWS account available and an [access_key and a secret_access_key pair generated](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html)
* Run `aws configure` to configure the aws-ci
* Install [Reflex](https://docs.reflexivesecurity.com/installation.html)
  * Docs also cover dependencies of Terraform and Python

### AWS Security with Native Tools

Full instructions can be found in [the native folder](native/)

### AWS Security with Open Source Tools

Full instructions can be found in [the reflex folder](reflex/)
