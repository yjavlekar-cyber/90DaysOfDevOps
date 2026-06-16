# Triggers & Matrix Builds
## Task 1: Trigger on Pull Request
- Created .github/workflows/pr-check.yml
- Created below yaml file which gets triggered when a pull request is opened against main.
  
      name: pull-request
    
      on:
        pull_request:
          branches: [ "main" ]
          types: [ "opened" ]
    
      jobs:
        print:
          runs-on: ubuntu-latest
      
          steps:
            - name: code checkout
              uses: "actions/checkout@v4"
      
            - name: prints branch confirmation
              run: echo "PR check running for branch ${{ github.head_ref }}"

  - Created a new branch using git checkout -b feature and pushed the code in that branch.
  - First pull was automatically created but after that i had to visit pull request to create new pull requests.
  - under the trigger on we have specificalyy used type opened which gets triggered when we manually create a pr request if we do not mention that on push also it gets triggered.
  - in yaml : are used to specify key:value pair hence if we use it anywhere in the script it will throw an error like when is was printing the branch i just used that thats why i faced error several times.

## Task 2: Scheduled Trigger
