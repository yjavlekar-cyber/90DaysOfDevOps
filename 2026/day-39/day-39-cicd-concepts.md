# What is CI/CD?
## Task 1: The Problem
    - Scenario
      Think about a team of 5 developers all pushing code to the same repo manually deploying to production.
      1) What can go wrong?
      If all 5 devlopers are pushing into a same repo and deploying it manually the last deployed changes wins.
      for example there is devloper A who has pushed the code and deployed after some time devloper b pushes his changes
      without considering the earlier code of dev A and deploys his code this will overwrite the devloper A's code.
    
      2)What does "it works on my machine" mean and why is it a real problem?
      In this problem if we consider there are 5 devlopers who have built and tested their code on their local and the same was deployed by each of them.
      So due to small here and there changes like file names,versions may lead the app to fail in production environment.
      This is because in manual deployment mainting such co-ordination becomes messy.

      3)How many times a day can a team safely deploy manually?
      For manual deployment the limit is usually once per day.


  ## Task 2: CI vs CD
  ### Continuous Integration — what happens, how often, what it catches
    - what happens
      Continuous Integration is the process where we integrate the source code into our main/master branch using version control system where every time
      a devloper pushes the code the automated CI triggers which first peroforms linting where we check the sytanx errors in our code,
      then we build our code into a reusable artifact which then gets tested if successful the artifact gets pushed to registry such as docker hub.
      If the test fails the build stage is marked as failed.
    
    - how often
      Every time a devloper pushes the code into main/master branch the CI gets triggered.
    
    - what it catches
      It basically compiles our code runs linting tests to check for syntax error in our code.
      After the build stage it again tests our artifacts if failed it notifies us.

  ### Continuous Delivery — how it's different from CI, what "delivery" means
    Continuous Delivery starts where Continuous Integration ends that is when the image is pushed to registry.
    In continuous Delivery we login to our registry pull the artifact and push it to our staging or prod envoirnment.
    Continous delivery requires manual interventation to get started.
    we can use this where we keep our code ready and manually we can deploy it at the future date whenever we want it to get applied.

  ### Continuous Deployment — how it differs from Delivery, when teams use it
      Continuous Deployement is same as delivery but the difference is that delivery requires manual trigger but
      deployment gets triggered automatically.
      This basically happens in real time whatever changes we will push those changes will get applied in real time.

## Task 3: Pipeline Anatomy
- Trigger: when we push the final code into github it starts the pipeline.
- Stage : stages are basically build,test and deploy suppose if our stage is build it will have steps related to building our artifact.
- Job : Inside the stage we have job like if we are in build stage we will have job to get the code do linting of the code.
- step : this is basically single commands which are required to perform the job.
- runner : bacially this can be on which OS this pipeline should run.
- Artifact: Is the output for e.g docker image.


## Task 4: Draw a Pipeline
     [ DEVELOPER ]
           |
           | (git push)
           v
     [ GITHUB REPO ] --(Trigger)--> [ RUNNER (Ubuntu) ]
                                           |
     +-------------------------------------|---------------------------------------+
     | PIEPELINE ANATOMY                   |                                       |
     |                                     v                                       |
     |  +-----------------------------------------------------------------------+  |
     |  |  STAGE 1: TEST (CI)                                                   |  |
     |  |  - Step: Run Linting (Check syntax)                                   |  |
     |  |  - Step: Run Unit Tests (Check logic)                                 |  |
     |  +----------------------------------|------------------------------------+  |
     |                                     |                                       |
     |                                     v                                       |
     |  +-----------------------------------------------------------------------+  |
     |  |  STAGE 2: BUILD (CI)                                                  |  |
     |  |  - Step: Docker Build (Create Image)                                  |  |
     |  |  - Step: Push to Docker Hub (Artifact Storage)                        |  |
     |  +----------------------------------|------------------------------------+  |
     |                                     |                                       |
     |               (Artifact: Docker Image "v1.0.1" in Registry)                 |
     |                                     |                                       |
     |                                     v                                       |
     |  +-----------------------------------------------------------------------+  |
     |  |  STAGE 3: DEPLOY (CD)                                                 |  |
     |  |  - Step: Login to Staging Server                                      |  |
     |  |  - Step: Docker Pull (Fetch latest image)                             |  |
     |  |  - Step: Docker Run (Start the app)                                   |  |
     |  +----------------------------------|------------------------------------+  |
     |                                     |                                       |
     +-------------------------------------|---------------------------------------+
                                           v
                                 [ STAGING ENVIRONMENT ]
                                     (App is Live!)


## Exploring the Pipeline

In below sample first we have trigger which gets triggered when the code is pushed of pull request is made.
Then we have used a build stage where in total we have three jobs.
Under job first we have used ubuntu OS as our runner.
Then we have steps which have commands to perform certain tasks like uses: actions/checkout@v4 which will check the code from repo.

    name: Test
    
    on:
      push:
        branches:
          - master
      pull_request:
        types: [opened, synchronize]
    
    jobs:
      # ==========================================
      # STAGE 1: Linting
      # ==========================================
      lint:
        name: Run Code Linting
        runs-on: ubuntu-latest
        steps:
          - name: Checkout Code
            uses: actions/checkout@v4
    
          - name: Set up Python
            uses: actions/setup-python@v5
            with:
              python-version: "3.10"
    
          - name: Install Dependencies
            run: pip install -r requirements.txt
    
          - name: Run Linting
            run: bash scripts/lint.sh
    
      # ==========================================
      # STAGE 2: Testing (Runs only if Lint passes)
      # ==========================================
      test:
        name: Run Pytest Suite
        runs-on: ubuntu-latest
        needs: lint # <-- Waits for lint stage
        steps:
          - name: Checkout Code
            uses: actions/checkout@v4
    
          - name: Set up Python
            uses: actions/setup-python@v5
            with:
              python-version: "3.10"
    
          - name: Install Dependencies
            run: pip install -r requirements.txt
    
          - name: Run Tests
            run: pytest
    
          # We must save the coverage files here before the runner destroys them
          - name: Temporarily Save Coverage Files
            uses: actions/upload-artifact@v4
            with:
              name: raw-coverage
              path: htmlcov/
    
      # ==========================================
      # STAGE 3: Artifact Upload (Runs only if Test passes)
      # ==========================================
      upload-coverage:
        name: Upload Coverage Artifact
        runs-on: ubuntu-latest
        needs: test # <-- Waits for test stage
        steps:
          # We download the files saved from the test job runner
          - name: Download Raw Coverage
            uses: actions/download-artifact@v4
            with:
              name: raw-coverage
              path: htmlcov/
    
          # This publishes the final artifact to your GitHub Actions run
          - name: Upload Coverage Artifact
            uses: actions/upload-artifact@v4
            with:
              name: coverage-report
              path: htmlcov/
