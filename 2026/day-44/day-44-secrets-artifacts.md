# Secrets, Artifacts & Running Real Tests in CI
## Task 1: GitHub Secrets
  - secrets in github actions are the credentials which we do not want to expose hence we store them in setiings> secrets & variables> actions.
  - This secrets are reusbale.
  - they have specific name under which we have stored this secrets.
  - In a script we can use them ${{ secrets.name_which_we_have_gave_for_secrets_in_settings }}
  - In this challenge we created a yaml which prints this secrets but we can see github actions doesnt reveal them those are printed as ***
  - Yaml:
    <img width="741" height="299" alt="image" src="https://github.com/user-attachments/assets/8838ba3c-0511-4baf-a5c3-8e7458c2b6da" />

  - Output on github actions:
    <img width="863" height="431" alt="image" src="https://github.com/user-attachments/assets/90cc1472-4990-4ff0-8be9-f8801b77385f" />

## Task 2: Use Secrets as Environment Variables.
  - Besides secrets there is another option called variables as secrets.
  - This variables are like env variables which we can store and reuse them as per requirment.
  - Just like in the below yml when we print those variables it shows what was the actual value stored in the settings.
  - They can be used as ${{ vars.name }}

  - yaml:
    <img width="648" height="334" alt="image" src="https://github.com/user-attachments/assets/b05a5b43-1857-47b2-90f9-da1cf4733a17" />


  -  Output:
    <img width="988" height="394" alt="image" src="https://github.com/user-attachments/assets/baaa87d9-1510-4a10-9828-e7bb4f58b094" />
  
## Task 3: Upload Artifacts
  - So in this we have created a yaml file which generates a txt files where we have redirected certain data.
  - then using github actions actions/upload-artifact@v4 which uploads this file as artifact on github actions.
  - This artifacts can be downloaded from github actions.
  - Yaml:
    <img width="573" height="477" alt="image" src="https://github.com/user-attachments/assets/b4ce4d9c-788e-4e29-8e31-9aa904ffb1c8" />

  - Output:
    <img width="1349" height="749" alt="image" src="https://github.com/user-attachments/assets/1bd5371a-2408-46ce-b32a-7798d0050dd0" />

## Task 4: Download Artifacts Between Jobs
  - In task 3 we created a file and using githubs action of upload, uploaded the same file on on github which we were able to download.
  - In this task we have used the same uploaded file download the same file in the yaml and print content from it.
  - so our job1 which is upload has script of uploading the artifact and job print has script related to dwonload and print contents of the file.
  - Yaml:
    <img width="890" height="809" alt="image" src="https://github.com/user-attachments/assets/8b697beb-d6a1-431b-aa5d-32484a0d6022" />
  - Output:
    <img width="914" height="564" alt="image" src="https://github.com/user-attachments/assets/ab224367-cbd7-49bc-b652-518c852eb538" />

## Task 5: Run Real Tests in CI
  - In this script we have a shell script which checks the health.
  - we first transfered our shell script inside .github/workflows.
  - then locally we have created a yaml which checkouts the code changes the permissions and executes the script.
  - key takeaway whenever we execute any script like this we neeed to mention the overall path like i have mentioned in the yaml.
  - yaml:
    <img width="608" height="373" alt="image" src="https://github.com/user-attachments/assets/8aaaa81a-f339-4bda-8434-fa7ddb6f22bd" />

  - output:
    <img width="1169" height="762" alt="image" src="https://github.com/user-attachments/assets/fb17c947-ec12-44ae-8b5b-c4e44f113071" />






