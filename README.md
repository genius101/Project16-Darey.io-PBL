# AUTOMATE INFRASTRUCTURE WITH IAC USING TERRAFORM PART 1

After you have built AWS infrastructure for 2 websites manually, it is time to automate the process using Terraform.

Let us start building the same set up with the power of Infrastructure as Code (IaC)

![tooling_project_16](https://user-images.githubusercontent.com/10243139/137618206-499335c6-0bef-4e15-b102-b2130cb0521e.png)

### Prerequisites before you begin writing Terraform code

- You must have completed Terraform course from the Learning dashboard

- Create an IAM user, name it terraform (ensure that the user has only programatic access to your AWS account) and grant this user AdministratorAccess permissions.

- Copy the secret access key and access key ID. Save them in a notepad temporarily.

- Configure programmatic access from your workstation to connect to AWS using the access keys copied above and a Python SDK (boto3). You must have Python 3.6 or higher on your workstation.

![P4](https://user-images.githubusercontent.com/10243139/137618211-31df33e2-8caa-4e39-b0a7-a66a114d6d66.png)

- Create an S3 bucket to store Terraform state file. You can name it something like yourname-dev-terraform-bucket

![P5](https://user-images.githubusercontent.com/10243139/137618228-26d6b027-4935-4281-9755-d746978ac315.png)

- When you have configured authentication and installed boto3, make sure you can programmatically access your AWS account by running following commands in python:

        import boto3
        s3 = boto3.resource('s3')
        for bucket in s3.buckets.all():
            print(bucket.name)

![P6](https://user-images.githubusercontent.com/10243139/137618233-a5bbc704-679b-4f38-8090-3086d8fbe661.png)


## Part 1 – VPC | Subnets | Security Groups

### Let us create a directory structure

Open your Visual Studio Code and:

- Create a folder called PBL

- Create a file in the folder, name it main.tf

Your setup should look like this:

![1b](https://user-images.githubusercontent.com/10243139/137618298-68d92f18-26d3-4222-b4e4-8d54e641be39.png)

Set up Terraform CLI as per this instruction below.

- Add AWS as a provider, and a resource to create a VPC in the main.tf file.

- Provider block informs Terraform that we intend to build infrastructure within AWS.

- Resource block will create a VPC.

        provider "aws" {
          region = "us-east-2"
        }

        # Create VPC
        resource "aws_vpc" "main" {
          cidr_block                     = "172.16.0.0/16"
          enable_dns_support             = "true"
          enable_dns_hostnames           = "true"
          enable_classiclink             = "false"
          enable_classiclink_dns_support = "false"
        }

![1c](https://user-images.githubusercontent.com/10243139/137618332-7144a484-485a-4f23-99f3-a870734b9a72.png)

The next thing is to download necessary plugins for Terraform to work. Lets accomplish this with terraform init command as seen in the below demonstration.

![1d](https://user-images.githubusercontent.com/10243139/137618349-cda7d5f4-af5f-4323-9374-3138c9d63560.png)

Next, let us create the only resource we just defined: aws_vpc.

Run terraform plan

![1e1](https://user-images.githubusercontent.com/10243139/137618371-19b411b0-c510-451b-a084-584db3994df2.png)

Then, if you are happy with changes planned, execute terraform apply

![1e2](https://user-images.githubusercontent.com/10243139/137618381-cb8faa6b-b8ae-40a2-99a7-3f4afdfc8000.png)

