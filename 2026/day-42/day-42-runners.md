# Runners: GitHub-Hosted & Self-Hosted
## Task 1: GitHub-Hosted Runners
- Created yaml file which gets triggered on push to main branch which runs on three different OS.
- In below sample file under jobs we have used three different jobs.
- where each job has a different OS as runner.
- and has steps where it outputs OS,hostname and current user.
  
      name: parallel
      
      on:
        push:
          branches: [ "main" ]
      
      jobs:
        first:
          runs-on: ubuntu-latest
      
          steps:
            - name: OS
              run: cat /etc/os-release
      
            - name: hots
              run: hostname
      
            - name: user
              run: whoami
        second:
          runs-on: windows-latest
      
          steps:
            - name: OS
              run: Get-CimInstance Win32_OperatingSystem | Select-Object Caption, Version, OSArchitecture
      
            - name: hots
              run: hostname
      
               - name: user
              run: whoami
      
        third:
          runs-on: macos-latest
      
          steps:
            - name: OS
              run: sw_vers
      
            - name: hots
              run: hostname
      
            - name: user
              run: whoami

## Task 2: Explore What's Pre-installed

    name: pre
    
    on:
      push:
        branches: [ "main" ]
    
    jobs:
      check:
        runs-on: ubuntu-latest
    
        steps:
          - name: docker version
            run: docker --version
    
          - name: python version
            run: python --version
    
          - name: node version
            run: node --version
    
          - name: git v
            run: git --version

- In above example i have used ubuntu as runner and printed the versions of docker, python, node and git which comes preinstalled with github hosted runners.
  
## Task 3: Set Up a Self-Hosted Runner 
- Instead of using runners provided by github actions this time saved my local machine into github actions as self hosted runner.
- In settings if we visit actions and then runners there we can click on new self hosted runner and it will give us the commands which we have to run on our terminal.
- Once the runner setup is done in settings>actions>runners we will be able to see our local machine as runner which is idle as of now because it is not in use.

## Task 4: Use Your Self-Hosted Runner
- As I have already created self-hosted runner created below yml which gets triggered on a push and uses self hosted runner which is my laptop.
  
      name: self
      on:
        push:
          branches: [ "main" ]
      jobs:
        self_os:
          runs-on: self-hosted
      
          steps:
            - name: host
              run: hostname
      
            - name: working dir
              run: pwd
      
            - name: new-file
              run: mkdir created-via-selfhosted-runner
- In above yml insted of using ubuntu we have used our self-hosted runner.
- we have assigned certain tasks like creating directory.
- once the task is completed successfully we can see in pwd we have created the directory as mentioned in yaml.
- Locally in our folder where we have the runner files if we run the run.sh it will show us live logs of the processes.
  
        yogesh_jawlekar@Profound:~/script/day41/actions-runner$ ./run.sh
        √ Connected to GitHub
        Current runner version: '2.335.1'
        2026-06-18 06:31:31Z: Listening for Jobs
        2026-06-18 06:33:13Z: Running job: self_os
        2026-06-18 06:33:26Z: Job self_os completed with result: Succeeded
## Task 5: Labels
- Basically labels are tagging/name which we give to our self hosted runners.
- This can be helpful when we have multiple runners.
- if we use only self hosted actions will get confused on which runner it should run the job.
  
       jobs:
        self_os:
          runs-on: [ self-hosted, my-linux-runner ]

  <img width="1200" height="562" alt="image" src="https://github.com/user-attachments/assets/91892f74-83f2-46c1-acef-ee8f6fca3bd6" />

  
## Task 6: GitHub-Hosted vs Self-Hosted

| Feature | GitHub-Hosted | Self-Hosted |
|----------|---------------|-------------|
| Who manages it? | GitHub | Your organization / team |
| Cost | Pay-per-use minutes (depending on plan) | Infrastructure and maintenance costs |
| Pre-installed tools | Many common tools and runtimes are pre-installed | You install and manage required tools yourself |
| Good for | Quick setup, small-to-medium projects, minimal maintenance | Custom environments, large workloads, compliance requirements |
| Security concern | Code and workflows run on GitHub-managed infrastructure | Full control over infrastructure, but you are responsible for securing it |



<img width="1364" height="519" alt="image" src="https://github.com/user-attachments/assets/63f04104-6331-4d11-88b2-a34900b00277" />


