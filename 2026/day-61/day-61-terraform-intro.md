# Introduction to Terraform and Your First AWS Infrastructure
## Task 1: Understand Infrastructure as Code
1.What is Infrastructure as Code (IaC)? Why does it matter in DevOps?
- IaC or infrastructure as a code basically means creating infrastructure by writing code.
- Manual way is very time consuming, lots of resources are required.
- In manual as we will be creating infrastructure there is high possibility that the created infra is not in sync which basically refers that this
  method is prone to errors.
- Devops basically means automation hence this automates the process of creation of infrastructure by writing code.

2.What problems does IaC solve compared to manually creating resources in the AWS console?
- version control
   - Now that we have our infrastructure in file formats or code it is very easy to keep track of versions of our infrastructure.
   - We can easily rollback with the help of this.
- idempotancy
   - IaC helps us deploy exactly same environment every time.
   - It first checks the code what is to be created.
   - Then it checks what is already been created
   - Then after the calculation it ignores what is already available and creates what is not available.
 
3.How is Terraform different from AWS CloudFormation, Ansible, and Pulumi?
- terraform uses hashi corp language for code which is also multi cloud.
- whereas cloud formation uses yaml and json and only supports on aws.
- pulumi uses python,go like programming languges and is multi-cloud.

4.What does it mean that Terraform is "declarative" and "cloud-agnostic"?
- Terraform is declarative because we have to declare our desired state of infrastructure.
- and we use terraform specifically to create infrastructure on cloud platforms hence it is also called as 'cloud-agnostic'.
  
## Task 2: Install Terraform and Configure AWS
- To install terraform we went to terraform website and copied the linux installation command and once installed to check we can run terraform -version.
- Then we have to first install aws cli by running aws configure
   - First we have to create a IAM user where we can create security credentials access key and secret key.
   - In our terminal we will run aws configure which will ask us for this keys once entered we are into aws cli.
   - To confirm we will run aws sts get-caller-identity.
 

## Task 3: Your First Terraform Config -- Create an S3 Bucket
- For this first we created a main.tf file which will hold our configuration for our resource and providers.
<img width="582" height="310" alt="image" src="https://github.com/user-attachments/assets/61da47e8-5497-4556-90bd-45320323170d" />

- where we have first declaraed our provider region and resources of aws which is s3_bucket and its name and arguments inside it with bucket name and tags.
- Once this is done we will run terraform init which will initilize the folder as terraform folder and create files terraform.tfstate  terraform.tfstate.backup
- Then after this once we apply this will apply the tf file by running terraform apply.
- at first i was getting error because the IAM user only had s3 read access once i gave the full access the bucket was created and we can confirm that on the aws console.

## Task 4: Add an EC2 Instance
<img width="1317" height="688" alt="image" src="https://github.com/user-attachments/assets/d336578d-55a8-4b4a-8da4-2970194368a4" />

- added one more resource block for ec2 instance with the vpc and subnet inside the ec2
- gave vpc policies
