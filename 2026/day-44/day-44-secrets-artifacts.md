# Secrets, Artifacts & Running Real Tests in CI
## Task 1: GitHub Secrets
  - secrets in github actions are the credentials which we do not want to expose hence we store them in setiings> secrets & variables> actions.
  - This secrets are reusbale.
  - they have specific name under which we have stored this secrets.
  - In a script we can use them ${{ secrets.name_which_we_have_gave_for_secrets_in_settings }}
  - In this challenge we created a yaml which prints this secrets but we can see github actions doesnt reveal them those are printed as ***
  - Yaml:
  - <img width="741" height="299" alt="image" src="https://github.com/user-attachments/assets/8838ba3c-0511-4baf-a5c3-8e7458c2b6da" />

  - Output on github actions:
  - <img width="863" height="431" alt="image" src="https://github.com/user-attachments/assets/90cc1472-4990-4ff0-8be9-f8801b77385f" />

## Task 2: Use Secrets as Environment Variables.
  - Besides secrets there is another option called variables as secrets.
  - This variables are like env variables which we can store and reuse them as per requirment.
  - Just like in the below yml when we print those variables it shows what was the actual value stored in the settings.
  - They can be used as ${{ vars.name }}
  - Yaml:
  - <img width="988" height="394" alt="image" src="https://github.com/user-attachments/assets/baaa87d9-1510-4a10-9828-e7bb4f58b094" />
  
  - output on github actions:
  - <img width="648" height="334" alt="image" src="https://github.com/user-attachments/assets/b05a5b43-1857-47b2-90f9-da1cf4733a17" />

