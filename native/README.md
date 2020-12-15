## AWS Security with Native Tools

### Prerequisites
* Manually create the bucket used for access logging.
  * In the aws_config.yaml template, I used `acuity-bucket-logs`

### Demo Setup

Create the CloudFormation stack with the aws-cli:

```
aws cloudformation create-stack --stack-name aws-config-rules --template-body file://cloudformation/aws_config.yaml --capabilities CAPABILITY_NAMED_IAM
aws cloudformation wait stack-create-complete --stack-name aws-config-rules
```

#### What will happen

To begin, you will see something like this as output to your `create-stack` command. This is the stack ID of the CloudFormation stack that was created. The second command will hang until the stack reaches the `CREATE_COMPLETE` status. You can also log in to [CloudFormation in the AWS Web Console](https://us-east-2.console.aws.amazon.com/cloudformation/home) to track the status. Please ensure you have selected the right region.

```
{
    "StackId": "arn:aws:cloudformation:us-east-2:140980722019:stack/aws-config-rules/57b8ca00-3e86-11eb-b524-026129d75bd2"
}
```

### Triggering Rules

The following aws-cli call will interact with the AWS API to create a very insecure bucket. Specifically, this bucket will not have access logging configured which is what our AWS Config rule is looking for.

```
aws s3api create-bucket --bucket really-insecure-bucket
```

#### What will happen

* After a while, you should recieve an email notifying you that the bucket we just created was found to be noncompliant.
* A few minutes later, you should see an update stating that the bucket was automatically remediated to become compliant.
  * The s3 bucket will be configured to start logging to the acuity-bucket-logs S3 bucket

### Demo Teardown

```
aws cloudformation delete-stack --stack-name aws-config-rules
aws cloudformation wait stack-delete-complete --stack-name aws-config-rules
```
