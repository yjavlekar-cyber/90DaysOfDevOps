# GitHub CLI: Manage GitHub from Your Terminal
## Task 1: Install and Authenticate
### 1.Install the GitHub CLI on your machine
    Installed on my linux ubuntu machine with following commands
    sudo apt update 
    sudo apt install gh -y

### 2.What authentication methods does gh support?
    Once gh is insatlled to run github on our CLI we need to login with our github account.
    For that we ran command  gh auth login which first asked 
                                      1.account type? github.com / github enterprise
                                      2.Preffered protocol? Https/ssh
                                      3.Want to activate with github credentials? Y/N
                                      4.How to authenticate Github CLI? login with web browser.

### 3.Verify you're logged in and check which account is active
    We can verify our account by using commands gh auth status
    which give us follwoing details:
                                  1.Logged in to which github.com
                                  2.Active account: true
                                  3.protocol
                                  4.Token
                                  5.Token scopes
                                  
## Task 2: Working with Repositories
### 1.Create a new GitHub repo directly from the terminal — make it public with a README
    To create new repo on github CLI we ran command gh repo create which operates interactively means it asks us questions and then creates a repo
                                    1.Create a new repository on GitHub from scratch / Create a new repository on GitHub from a template repository / Push an existing local repository to GitHub
                                    - Selected new repo from scratch.
                                    2.Then repository name
                                    3.Description
                                    4.Visibility? Public / private / Internal
                                    - selected Public
                                    5.Then it asks us to create Readme file or not?
                                    - Yes
                                    6.Then whether to add .gitignore or not?
                                    - NO
                                    7.whether to add license or not?
                                    - Yes
                                    8.Then it will ask wether to clone the repository locally or not?
                                    - Y means it will be available on local as well as on remote
                                    - N means will be available only on remote
### 2.Clone a repo using gh instead of git clone
    By above process we only created a repo from CLI onto our github remote but it will not show on our CLI
    for that to show on our CLI we need to clone it by using:
    gh repo clone <on github we will get a github CLI link that we have to use here>

