# Variables, Outputs, Data Sources and Expressions
## Task 1: Extract Variables
- Instead of hardcoding values directly in our main.tf we created a varibles.tf which will have all the values.
- The actual value which we set is by the keyword default also we have to mention type which are are as follow:
  - string (which is basically a name or any aplhabetical keyword)
  - number
  - bool
  - list
  - map
- In this we have also mentioned project name but the vaule is not set to default that is the reason when we do terraform plan it asks for the the project name as well.
  
<img width="1273" height="740" alt="image" src="https://github.com/user-attachments/assets/35f200bd-f30a-4d93-910b-51e261b40610" />

## Task 2: Variable Files and Precedence
- Earlier to avoid the hardcoding we created variables.tf file.
- But what if we want more than set two or more values to a specific vairbale like environment
- In that case we created a terrafomr.tfvars file which has our environment-dev and another tfvars with environment-production.
- so when we do terraform plan by default it uses terraform.tfvars but with that if we use -var-file=filename it will use that file.

## Task 3: Add Outputs
- Now that we have tfvars file before applying we will select which tfvar file should be used by doing terraform plan with it.
- and then we will do terraform apply
- We have also created one outputs.tf which lists certain outputs and from their value should be derived
- once we apply and when we do terraform output it gives us the values for those listed variables on our cli it self.

<img width="949" height="689" alt="image" src="https://github.com/user-attachments/assets/88ea1257-5d10-4f06-adb5-2b71e8a5570b" />

## Task 4: Use Data Sources
- In this part inside our main.tf above the resources we declare data which exactly works like variables but instead of creating another variables.tf but only mention in main and use it there only.
- In here we have used data for ami with filters of name,virtulization and root device type and and availablity zones which inside our instance we declare the very first available zone.

<img width="709" height="442" alt="image" src="https://github.com/user-attachments/assets/335e1694-ce35-46c2-80e7-f6339c93c349" />

### What is the difference between a resource and a data source?
- Resource
    - A resource is an infrastructure object that you want Terraform to create, modify, or destroy in your cloud provider
- data
    - A data source allows Terraform to look up or fetch information about resources that already exist outside of your current Terraform code.
so when i change the region as the ami is constant it will automatically fetch the first available zones

## Task 5: Use Locals for Dynamic Values
- we now have variable.tf for values which can only be one.
- Then tfvars files for values such as env which can be more than one
- this above two we can directly use in the main.tf but what if after that we if in main.tf we want to change more values we cannot change directly inside the tfvars or var.
- instead of that we use a local block inside main.tf where we refer the values from variable.tf and applies for the whole code.
- in this particular example we have used this for a constant name tag for every resource.

<img width="1350" height="987" alt="image" src="https://github.com/user-attachments/assets/d298b37d-35c2-4d83-8138-5b89899ea69b" />

## Task 6: Built-in Functions and Conditional Expressions
- if we run terraform console in our shell it opens up an interactive terminal which we can use to fetch values of variables and also we can use several functions and conditional expressions
- string functions like upper converts string into uppercase then join function joins more than one strings provided,
- then there are collection functions such as lenght which calculates length, lookup to search and toset to remove to remove duplicates.
- also networking functions such as cidrsubnet("10.0.0.0/16", 8, 1)

# 🗺️ The Terraform Data Flow
 ┌───────────────────────────┐         ┌───────────────────────────┐
 │   1. USER DATA CONTENT    │         │  2. LIVE CLOUD REALITIES  │
 │  (Changes per deployment) │         │   (Controlled by the API) │
 └─────────────┬─────────────┘         └─────────────┬─────────────┘
               │                                     │
               ▼                                     ▼
 ┌───────────────────────────┐         ┌───────────────────────────┐
 │     terraform.tfvars      │         │          data.tf          │
 │   project_name = "ecom"   │         │ data "aws_ami" "linux"    │
 │   environment  = "dev"    │         │ data "aws_az" "available" │
 └─────────────┬─────────────┘         └─────────────┬─────────────┘
               │                                     │
               ▼                                     │
 ┌───────────────────────────┐                       │
 │       variables.tf        │                       │
 │  Checks types, validates  │                       │
 │  inputs from .tfvars file │                       │
 └─────────────┬─────────────┘                       │
               │                                     │
               ▼                                     │
 ┌───────────────────────────┐                       │
 │         locals.tf         │                       │
 │  Combines & fixes formatting │                    │
 │  name_prefix = "ecom-dev" │                       │
 └─────────────┬─────────────┘                       │
               │                                     │
               └───────────────────┬─────────────────┘
                                   │
                                   ▼
 ┌─────────────────────────────────────────────────────────────────┐
 │                            main.tf                              │
 │                                                                 │
 │   resource "aws_subnet" "sub-main" {                            │
 │     vpc_id            = aws_vpc.main.id                         │
 │     cidr_block        = var.subnet_cidr          ◄── [From Var] │
 │     availability_zone = data.aws_az.names[0]     ◄── [From Data]│
 │     tags = {                                                    │
 │       Name = "${local.name_prefix}-subnet"       ◄── [From Local]│
 │     }                                                           │
 │   }                                                             │
 └─────────────────────────────────────────────────────────────────┘

## 🪵 Breakdown of the Journey
### 🏭 Phase 1: Input InjectionData starts at terraform.tfvars where you supply environment-specific configurations (e.g., environment = "dev").This data is validated by your blueprint settings in variables.tf to verify it is safe to use.🏗️ 
### Phase 2: Internal RefineryBecause you can't run computations inside .tfvars, the validated variables enter the locals block.Here, the code engine combines the strings into a single standard naming pattern ("ecom-dev"), shielding your resources from repetitive updates.
### 📡 Phase 3: Cloud SynchronizationConcurrently, data blocks send a real-time read-only query to AWS.They return active infrastructure facts like live AMI IDs and current Availability Zone layouts directly into memory.
### 🚀 Phase 4: Main ConstructionEverything converges in main.tf.The resource blocks pick their pieces from the dynamic conveyor belt—injecting variables for networking, data sources for cloud placement, and locals for consistent infrastructure tagging.
