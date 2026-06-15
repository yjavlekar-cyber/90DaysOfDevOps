# My First GitHub Actions Workflow
## Task 1: Set Up
- created a new public repository on github called github-actions-practice.
- using git clone https cloned the repository on my local machine.
- using mkdir -p created .github/workflows/ inside the repo.

## Task 2: Hello Workflow
Created hello.yml inside .github/workflows/.

     name: hello
      on:
        push:
          branches: [ "main" ]
      
      jobs:
      greet:
        runs-on: ubuntu-latest
    
        steps:
          - name: code checkout
            uses: "actions/checkout@v4"
    
          - name: print hello
            run: echo "Hello from GitHub Actions!"


## Understanding the Anatomy
- on: on is our trigger point which gets activated every time we push from our local to remote repositories main branch.
- jobs: is the set of instructions which we want to carry out.
- runs-on: To carry out the instructions inside we also need an OS which we mention here in runs-on.
- steps: This includes the step-by-step commands which will help achieve our goal.
- name: this is a made-up name which we provide to our steps.
- uses: These are pre-defined actions provided by github which are reusable like to checkout code we used actions/checkout@v4
- run: to run certain commands we can use run like we have used to echo our output.

## Add More Steps
Added more steps:
- name: Print current date and time
  run: echo $(date)

- name: branch name
  run: echo "The current branch is ${{ github.ref_name }}"


- name: list files
  run: ls -R

- name: runners OS
  run: cat /etc/os-release


## Issues faced
The issues were mostly sytnax relates like:
- In trigger the branch was not in double qoutes.
- runs-on which i used was runs_on which was incorrect.
- used semi colons to seprate the runner like ubuntu:latest which was wrong correct way was ubuntu-latest
- The predefined actions should be double qoutes.
- using uses for linux commands like echo where i should have used run which was rectified.
