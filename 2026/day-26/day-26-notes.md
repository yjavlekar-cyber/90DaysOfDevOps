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

### 3.View details of one of your repos from the terminal
    To view the details of our repo first we need to add the origin by using  git remote add origin https://github.com/yjavlekar-cyber/New_Repo.git
    This only we have to do if we have said N to clone the repo locally while creating repo if yes then no issue.
    Once done we can run gh repo view.
    Which will give us result 
    yogesh_jawlekar@Profound:~/script/day24$ gh repo view
    yjavlekar-cyber/New_Repo
    This is a new repo created to study Github CLI
    
    
       New_Repo
    
      This is a new repo created to study Github CLI
    
    
    
    View this repository on GitHub: https://github.com/yjavlekar-cyber/New_Repo
### 4.List all your repositories
    For this we ran gh repo list
    yogesh_jawlekar@Profound:~/script/day24$ gh repo list
    
    Showing 10 of 10 repositories in @yjavlekar-cyber
    
    NAME                                                            DESCRIPTION                                                                               INFO          UPDATED
    yjavlekar-cyber/90DaysOfDevOps                                  This repository is a Challenge for the DevOps Community to get stronger in DevOps.The...  public, fork  about 9 minutes ago
    yjavlekar-cyber/New_Repo                                        This is a new repo created to study Github CLI                                            public        about 23 minutes ago
    yjavlekar-cyber/gitpractice                                     This is repo made while practicing git commands.                                          public        about 2 days ago
    yjavlekar-cyber/Audio-analyzer                                                                                                                            public        about 16 days ago
    yjavlekar-cyber/project-2-fastapi                               This is basic jenking API project.                                                        public        about 17 days ago
    yjavlekar-cyber/Website                                         Deployment of website                                                                     public        about 18 days ago
    yjavlekar-cyber/learning-github-actions                         from zero to hero                                                                         public        about 18 days ago
    yjavlekar-cyber/system-health-monitor-                                                                                                                    public        about 20 days ago
    yjavlekar-cyber/my-tickets-app                                                                                                                            public        about 1 month ago
    yjavlekar-cyber/https-github.com-bregman-arie-devops-exercises                                                                                            public, fork  about 4 years ago

### 5.Open a repo in your browser directly from the terminal
    We can open repo on two ways:
    1.gh repo view <link> Only to view.
    2.gh repo clone <link> To start working

### 6.Delete the test repo you created (be careful!)
    To delete we can use gh repo delete <link>
    This happened because deleting a repository is a "high-risk" action. By default, the GitHub CLI does not have permission to delete things, even if you are logged in. This protects you from accidentally
      deleting a repo via a script or a typo.
    
      To fix this, you need to grant the CLI the delete_repo permission (scope).
    
      1. Run the Refresh Command
      Copy and paste the exact command the error gave you:
    
       1 gh auth refresh -h github.com -s delete_repo
    
      2. What will happen:
       * It will ask: ! First-party GitHub CLI GitHub App is already authorized. To add 'delete_repo' scope, we need to re-authorize.
       * Press Enter to open your browser (or follow the code prompt if you are on a remote server).
       * On the GitHub website, click "Authorize github".
       * Your terminal will then say ✓ Authentication complete.
    
      3. Delete the Repo again
      Now that you have the "keys" to delete, run your command again:
    
       1 gh repo delete yjavlekar-cyber/New_Repo
    
      It should work perfectly this time!

## Task 3: Issues
### 1.Create an issue on one of your repos from the terminal — give it a title, body, and a label
    Issues in github basically means tickets created for bug change and new feature etc.
    To create we can ran below command
    gh issue create --title "Bug in login" --body "Login fails on invalid token"  
    
    --title - being the title of the issue and --body being the main matter of the issue.

### 2.List all open issues on that repo
    To list all the issues we can ran 
    gh issue list  

### 3.View a specific issue by its number
    To list the issue with its number 
    gh issue view 1
    
    yogesh_jawlekar@Profound:~/script/day24$ gh issue view 1
    Bug in login yjavlekar-cyber/New_Repo#1
    Open • yjavlekar-cyber opened about 39 minutes ago • 0 comments
    
    
      Login fails on invalid token
    
    
    View this issue on GitHub: https://github.com/yjavlekar-cyber/New_Repo/issues/1

    To opne the issue in web browser
    gh issue view 1 --web4
    This will directly open the issue on web browser.
    
### 4.Close an issue from the terminal
    To close the issue 
    gh issue close 1
    yogesh_jawlekar@Profound:~/script/day24$ gh issue close 1
    ✓ Closed issue yjavlekar-cyber/New_Repo#1 (Bug in login)
    
### 5.How could you use gh issue in a script or automation?
    1.we can use issue in script where if the script fails issue shall be created automatically
     ./run_tests.sh
    if [ $? -ne 0 ]; then
    echo "Tests failed! Creating an issue..."
    gh issue create --title "Build Failure: $(date)" --body "The automated tests failed on the server. Please check the logs." --label "bug,automated-report"
    fi
