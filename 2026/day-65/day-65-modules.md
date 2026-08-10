# Terraform Modules: Build Reusable Infrastructure
## Creating child modules and root modules
- First created a folder structure like below which first has our root module and inside modules we have blueprints for ec2 and security groups.
<img width="758" height="349" alt="image" src="https://github.com/user-attachments/assets/eaac2540-2a4a-4c69-90b1-dd3a2aa2845d" />

### working of this structure

### Child modules
- we first created our modules which are ec2 and security groups.
- created variables.tf which will have all the variables which are required to created our resources.
- then we created a main.tf where we have assigned values to all the data points from variables like var.ami_id etc
  
*ec2-child-module*
<img width="1641" height="909" alt="image" src="https://github.com/user-attachments/assets/36eb0dcc-8ad5-42c5-bf6d-5de19579fe1d" />

*security-group-child-module*
<img width="1398" height="991" alt="image" src="https://github.com/user-attachments/assets/03b7474c-9aac-4e32-aa24-e3530282148a" />


### Root modules
- In root module we created providers.tf with required provides and region.
<img width="1135" height="240" alt="image" src="https://github.com/user-attachments/assets/27cf982a-ede2-4a5d-ba84-0e65303980f8" />

- Then we created a main.tf with below listed configuration
  - we first declared local variables which we will be using only inside the main.tf
  - then data blocks which will carry values for ami,availability zones.
  - then vpc resource and a subnet resource using same vpc.
  - Then we have to create security group and two servers basically two instances
  - for this we will not use resource block but we will use module block which will call the modules declared
<img width="997" height="590" alt="image" src="https://github.com/user-attachments/assets/e322c468-21e0-4f6e-9466-0b6661fd2619" />

- So to first we run terraform init then terraform plan and lastly terraform apply
- We first have our variables.tf and main.tf which has actuall resource blocks but there are no values mapped to those variables.
- but when we create a root module in that main.tf we will assign them variables directly,with help of locals or data blocks.
- and when we apply the same that value will be fetched by the variable.tf inside child module and then used by the main.tf inside the child module.
