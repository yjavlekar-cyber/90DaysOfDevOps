# Secrets, Artifacts & Running Real Tests in CI
## Task 1: GitHub Secrets
  - secrets in github actions are the credentials which we do not want to expose hence we store them in setiings> secrets & variables> actions.
  - This secrets are reusbale.
  - they have specific name under which we have stored this secrets.
  - In a script we can use them ${{ secrets.name_which_we_have_gave_for_secrets_in_settings }}
  - In this challenge we created a yaml which prints this secrets but we can see github actions doesnt reveal them.
  - Yaml:
  - <img width="741" height="299" alt="image" src="https://github.com/user-attachments/assets/8838ba3c-0511-4baf-a5c3-8e7458c2b6da" />

  - Output on github actions:
  - <img width="863" height="431" alt="image" src="https://github.com/user-attachments/assets/90cc1472-4990-4ff0-8be9-f8801b77385f" />
