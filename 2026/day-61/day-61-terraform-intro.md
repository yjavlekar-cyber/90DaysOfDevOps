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
  
