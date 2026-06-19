# Jobs, Steps, Env Vars & Conditionals
## Multi-Job Workflow
- In this workflow we have created three different jobs under one job.
- This workflow gets triggerd when we push it to our github.
- All the three jobs runs-on ubuntu-latest which is githubs own runner.
  
      name: multi-jobs
      on:
        push:
          branches: [ "main" ]
      jobs:
        build:
          runs-on: ubuntu-latest
          steps:
            - name: print
              run: echo "building the app"
        test:
          runs-on: ubuntu-latest
          steps:
            - name: test
              run: echo "Running tests"
        deploy:
          runs-on: ubuntu-latest
          steps:
            - name: deploy
              run: echo "Deploying"

  <img width="1151" height="565" alt="image" src="https://github.com/user-attachments/assets/d14dd1a7-e91d-4a32-bfe9-99ab7354185e" />

## Environment Variables
- Instead of hardcoding we can also use variables in the script.
- variables can be defined by using keywords-env.
- There are two types of variables
  - 1) first which are defined by us in the script.
    2) second ones are githubs own variables which are predefined and are called "github context variables"
       some of the examples are as follows:
       - 1. Git & Repository Context
            These variables contain data about the code repository, branches, commits, and actions.
            - 1) ${{ github.repository }}: The owner and repository name (e.g., octocat/hello-world).
              2) ${{ github.ref_name }}: The short branch or tag name that triggered the run (e.g., main or v1.0.0)
              3) ${{ github.sha }}: The full 40-character commit SHA hash that triggered the workflow.
              4) ${{ github.actor }}: The GitHub username of the person who triggered the run.
              5) ${{ github.event_name }}: The name of the event that triggered the run (e.g., push, pull_request, workflow_dispatch).
       - 2. Runner Environment Context
            These variables give you details about the virtual machine executing your job.
            - 1) ${{ runner.os }}: The operating system of the runner (returns Linux, Windows, or macOS).
              2) ${{ runner.arch }}: The architecture of the runner (returns X64, ARM, or ARM64).
              3) ${{ runner.temp }}: The path to a temporary directory on the runner that resets after every job.
       - 3. Workflow & Matrix Contexts
            These help you track current runs or manage parallel test parameters.
            - 1) ${{ github.run_id }}: A unique number assigned to every specific workflow run (useful for creating distinct logs or tracking builds).
              2) ${{ github.run_number }}: A counter that increments by 1 for each run of this specific workflow (e.g., Run #1, Run #2).
              3) ${{ matrix.<key> }}: The current value of a matrix property if you are running multi-configuration testing.
      - 4. Security & Configuration Contexts
           These look up secure data stored in your GitHub repository settings.
           - 1) ${{ secrets.YOUR_SECRET_NAME }}: Accesses encrypted tokens, API keys, or passwords.
             2) ${{ vars.YOUR_VARIABLE_NAME }}: Accesses non-sensitive configuration text stored at the repository or environment level.

- below is the yml file created by me to practice this:
  
      name: variable
      on:
        push:
          branches: [ "main" ]
      env:
        APP_NAME: myapp
      jobs:
        variables_list:
          runs-on: ubuntu-latest
          env:
            ENVIRONMENT: staging
          steps:
            - name: print all variables and contexts.
              env:
                VERSION: 1.0.0
              run: |
                echo "--------------------------------"
                echo "workflow level(App name): $APP_NAME"
                echo "job level(Environment): $ENVIRONMENT"
                echo "Step level(version): $VERSION"
                echo "_______________________________"
                echo ""
                echo "Github context variables"
                echo "commit SHA: ${{ github.sha }}"
                echo "Triggered by(actor): ${{ github.actor }}"
                echo "-------------------------------"

<img width="1114" height="574" alt="image" src="https://github.com/user-attachments/assets/071d9f9a-0d87-45d2-9cce-aaa31ddc9bc4" />
