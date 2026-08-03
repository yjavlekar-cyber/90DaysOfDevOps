# Terraform State Management and Remote Backends
## Task 1: Inspect Your Current State
- First applied a main.tf which creates a instance,vpc and s3 bucket.
- to inspect the current state we can run below commands:
  - terraform show - This shows our whole configuration for our state file.
  - terraform state list - Whatever resources we create that we can list down by using this.
  - terraform state show nameofthresource - We can view state of our individual resources.

- How many resources does Terraform track?
  - Terraform tracks all the resources created using main.tf for now this are 3.
- What attributes does the state store for an EC2 instance? (hint: way more than what you defined)
 - Yes when we created ec2 we only mentioned the ami,instance type and tags but when we do terraform state show we can see many attributes such azs etc listed.
- Open terraform.tfstate in an editor -- find the serial number. What does it represent?
 - Whenever we run terraform apply the first time it creates a statefile with serial number 0 and gradually with every update the number gets added.

## Task 2: Set Up S3 Remote Backend
- Setting up backend basically refers to creating a resource for s3 bucket where we will store our terraform.tfstate our statefile.
- Keeping our statefile locally is very dangerous because if the state file gets deleted we will lose everything created on our cloud hence we will store the file in our bucket.
- and once the file is moved to bucket locally we can't see our file.
- for this task we alreay had our resources created on our aws we created a seprate .tf file which creates a s3 bucket then resource for versioning of that bucket and resource for dynamodb table.
- once we have this we will run terraform init which will initilize our backend and ask us wether we want to copy locally existing state file into backend which is our s3 and dynamodb table.

<img width="1503" height="437" alt="image" src="https://github.com/user-attachments/assets/6366b451-d0fb-4985-a3d5-eefb774a2f6e" />

## Task 3: Test State Locking
State locking prevents when two people at the same time try to edit the statefile it will store the logs of whoever is currently editing the file and will lock the file if any other user tried to edit on the same time.
- To test this we opened two terminals for the same project.
- In the first one we run terraform plan
- and for the second we run terraform apply
- while the first terminal is running  plan if we run suppose terraform apply it will show us that the statfile is locked as another terminal is also running some commands there.
<img width="1145" height="498" alt="image" src="https://github.com/user-attachments/assets/14e170dc-409d-47d7-896e-3d372ad05b88" />

## Task 4: Import an Existing Resource
- We can even import the already available resources from aws on to our statefile
- for this task first we created an another bucket on aws.
- Then in our main.tf we added that as a resource.
- Then we run terraform import resource resource-name bucketname-onaws
- after this if we run terraform state list we can see our bucket is also available which we imported.
<img width="1377" height="713" alt="image" src="https://github.com/user-attachments/assets/588268bc-cae5-4b26-a8aa-ec5fa659139e" />


## Task 5: State Surgery -- mv and rm
- mv
  - We can also move or remove our resources individually.
  - To rename the current s3 bucket we ran mv command with resource.current-name resource.new-name as mentioned in attched snap shot.
  <img width="1485" height="575" alt="image" src="https://github.com/user-attachments/assets/08905e2e-f535-41e9-bfa6-09c3ba25a9f2" />
  - And if we also want to change the same on aws we can change the name in our resource as well.
- rm
  - We can even remove our resources locally by running terraform state rm resource.name.
    
  <img width="1264" height="547" alt="image" src="https://github.com/user-attachments/assets/df6f206b-ab83-4fff-bad7-08245f1746ff" />

## Task 6: Simulate and Fix State Drift
State drift happens when someone changes infrastructure outside of Terraform -- through the AWS console, CLI, or another tool.

- To test this we first change name of ec2 instance through our aws console.
- Then if we run terraform plan it shows us the changes which are there which means the drift between our infrastructure on cloud and in statefile.
- now we have two options we can either change our main.tf to apply the changes locally as well.
- also if we dont change anything and just run terraform apply we can see the terraform again changes to name to match our state file.

<img width="1517" height="709" alt="image" src="https://github.com/user-attachments/assets/7ac15d48-6182-4d56-bdfc-635907159fcf" />


