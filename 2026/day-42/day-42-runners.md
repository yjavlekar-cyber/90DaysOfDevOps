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
  

