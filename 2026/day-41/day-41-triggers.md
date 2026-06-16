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
- If we want any workflow to trigger on specific time we will use below trigger of cron job.

      name: scheduled
      on:
        schedule:
          - cron: "52 15 * * *"



## Task 3: Manual Trigger
- To trigger workflows manually we will use on workflow dispatch as we have used in below yaml.
- Through this we can manually start the workflow we can go to actions and at the right side corner click on run workflows.

       name: hello
       on:
        workflow_dispatch:

  
## Task 4: Matrix Builds
- In matrix strategy we can run the workflows on different versions of our runners.

        name: checking
        
        on:
          push:
            branches: [ "main" ]
        
        jobs:
          new:
           strategy:
            matrix:
              version: [ 10,12,14 ]
              os: [ ubuntu-latest ]
        
           runs-on: ${{ matrix.os }}
        
           steps:
              - name: os
                run : echo "cat /etc/os-release"

- Just like in above example we have used strategy which is matrix under which three different veriosn of os ubuntu-latest we have used.
- and then we have used runs-on with matrix.os variable
- Once the workflow is triggered we can see three different workflow runs under github actions.


## Task 5: Exclude & Fail-Fast

     name: checking
    
     on:
       push:
         branches: [ "main" ]
    
     jobs:
       new:
         strategy:
          fail-fast: false  # If one job fails, the others will NOT be cancelled
          matrix:
            version: [ 10, 12, 14 ]
            os: [ ubuntu-latest, windows-latest ] # Added an OS to make 'exclude' meaningful
   
            exclude:
              - os: windows-latest
                version: 10  # This specific combination will be skipped
   
        runs-on: ${{ matrix.os }}
   
        steps:
           - name: os check
             run: echo "Running version ${{ matrix.version }} on ${{ matrix.os }}"

- In the above example we have used two strategies under matrix first is fail-fast and then exclude.
- by default github stops all jobs if any one of the job fails.
- by using fail-fast: false we make sure that even one job fails other ones will continue.
- we have also used except which will exclude that specific version that version will not run its workflow.
