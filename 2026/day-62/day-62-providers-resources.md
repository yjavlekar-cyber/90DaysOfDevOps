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
- In this task we have created a main.tf file which creates vpc and other resources on aws as mentioned below:
  1. vpc - our private virtual cloud
  2. subnet - which takes vpc_id and cidr and value set to true to map public ip on lunch.
  3. Internet gateway - To connect to the outside internet with earlier created vpc_id.
  4. route tables - this basically maps an IP through which our exiting traffic will leave the vpc in much broader sense we have public ec2 instance trffice will first have that ip and when it leaves
     internet gateway will swap the ip with this IP.
  5.route_table_association - This resource block basically maps our route table to our subnet

<img width="1136" height="810" alt="maintf" src="https://github.com/user-attachments/assets/31be2d0f-7d17-460b-bf90-d5e02a4af98a" />


<img width="1892" height="1010" alt="plan" src="https://github.com/user-attachments/assets/068559a7-0e60-46a8-964c-8363961f4b47" />


1.How does Terraform know to create the VPC before the subnet?
- terraform does not read our main.tf in top to bottom before execution it creates a graph so as in subnet we have used .id in vpc_id which by defults denoted that the subnet is inside the vpc accordingly that it creates.
  
2.What would happen if you tried to create the subnet before the VPC existed?
- It will give us an api call error.
  
3.Find all implicit dependencies in your config and list them

        [aws_vpc.main]
           │
           ├──> [aws_subnet.sub-main] ──────────────┐
           ├──> [aws_internet_gateway.ig]            │
           ├──> [aws_security_group.web_traffic]     │
           │                                         │
           └──> [aws_route_table.route] <────────────┤
                       │                             │
                       ▼                             ▼
           [aws_route_table_association]       [aws_instance.web_server]


## Task 4: Add a Security Group and EC2 Instance
- In this task we created a security group which refrences to our vpc and allows ingress for ssh and http and all egress traffic.
- Then we created a ec2 instance which references to subnet and our security groups.

<img width="1052" height="837" alt="image" src="https://github.com/user-attachments/assets/84660077-11c6-48e0-a7d4-a1b73743a6eb" />

- also added one s3 bucket which depends on ec2

<img width="1192" height="215" alt="image" src="https://github.com/user-attachments/assets/b7049a45-9e48-43ef-9277-98c4b7154009" />

## Task 6: Lifecycle Rules and Destroy
- In our ec2 we added one block of lifecycle which detects any changes and deletes old one and then creates new one.
- Three different lifecycles are create_before_destroy, prevent_destroy, ignore_changes.

<img width="1406" height="684" alt="image" src="https://github.com/user-attachments/assets/03019c78-9e40-44a2-a70c-9bfc370f01d6" />

- To destroy we run terraform destory.
