# Task 1: Explore the AWS Provider
- Created a providers block which installs specific version and uses a defined aws region.

        yogesh_jawlekar@Profound:~/script/terra-practice/terraform-aws-infra$ cat providers.tf
        terraform {
                required_providers {
                        aws = {
                                source = "hashicorp/aws"
                                version = "~> 5.0"
                        }
                }
        }
        
        provider "aws" {
                region = "us-west-1"
        }
- Then we run terraform init which initilizes terraform.
- If we see the file .terraform.lock.hcl
     - we can see our provider which is aws
     - then our current version of aws
     - after that constraint version
- What does ~> 5.0 mean? How is it different from >= 5.0 and = 5.0.0?
   - The ~> symbol refers to pessimistic constraint operator which gets the bug fixes and adds features but stops major update.
   - Here we have used ~> 5.0 so it can only use till 5.100 it will not go to 6.0.0
  
<img width="1382" height="974" alt="image" src="https://github.com/user-attachments/assets/509b7478-c1e7-4162-aea5-4b0d3dd7eeb5" />

## Task 2: Build a VPC from Scratch
