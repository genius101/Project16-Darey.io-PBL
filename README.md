# AUTOMATE INFRASTRUCTURE WITH IAC USING TERRAFORM PART 1

After you have built AWS infrastructure for 2 websites manually, it is time to automate the process using Terraform.

Let us start building the same set up with the power of Infrastructure as Code (IaC)

Prerequisites before you begin writing Terraform code

1. You must have completed Terraform course from the Learning dashboard(Done:Tick)

2. Create an IAM user, name it terraform (ensure that the user has only programatic access to your AWS account) and grant this user AdministratorAccess permissions.(Done:Tick)

3. Copy the secret access key and access key ID. Save them in a notepad temporarily.(Done:Tick)

4. Configure programmatic access from your workstation to connect to AWS using the access keys copied above and a Python SDK (boto3). You must have Python 3.6 or higher on your workstation.(Done:Tick)

5. Create an S3 bucket to store Terraform state file. You can name it something like <yourname>-dev-terraform-bucket (Done:Tick)

6. When you have configured authentication and installed boto3, make sure you can programmatically access your AWS account by running following commands in >python:

import boto3
s3 = boto3.resource('s3')
for bucket in s3.buckets.all():
    print(bucket.name)

