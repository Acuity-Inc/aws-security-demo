## AWS Security with Open Source Tools

### Prerequisites
* Manually create the bucket for the S3 backend that tracks Terraform state.
  * In the reflex.yaml.example, I used `acuity-aws-security`
* Ensure a [CloudTrail](https://aws.amazon.com/cloudtrail/) has been configured for the account.

### Demo Setup

Generate the Reflex config file (reflex.yaml). An example configuration file exists so you can see how it configure it.

```
reflex init
```

Generate the deployment packages which are the zip files of the lambdas that will be uploaded to AWS via Terraform.

```
reflex package
```

Generate the Terraform modules that will be deployed with Terraform.

```
reflex build
```

Finally, run Terraform to apply the configuration

```
cd reflex_out
terrform init
terraform apply
```

#### What will happen

Terraform will generate the state file and look at the current state of the AWS account using the AWS APIs. After assessment is complete, it will spit out a list of AWS resources it determined that it needed to create in order to deploy our configuration as we demanded. It will prompt you to confirm that it is OK to proceed. Type `Y` and then hit enter to continue. Terraform will take several minutes to run for the first time.


### Triggering Rules

The following aws-cli call will interact with the AWS API to create a very insecure bucket. Specifically, this bucket will not have encryption configured which is what our AWS Config rule is looking for.

```
aws s3api create-bucket --bucket really-insecure-bucket
```

#### What will happen

* Almost immediately you should recieve an email notifying you that the bucket we just created was found to be noncompliant and that it was immediately remediated to become compliant.
  * The s3 bucket will be configured to encrypt objects using the default [KMS key](https://aws.amazon.com/kms) for S3.

### Demo Teardown

```
terraform destroy
```
