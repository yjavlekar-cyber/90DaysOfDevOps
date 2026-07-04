# GitHub Actions Project: End-to-End CI/CD Pipeline
## About the code
- main.py This contains our app logic based on fast API.
- Then we have requirements.txt which consists our requirements for main logic.
- test_main.py this file allows us to run tests on our code using pytest.

## Task 1: Set Up the Project Repo
- Created a new repository on github.
- then initiated git repository in our project.
- then via set-url connected remote and local repo.
- Created a Dockerfile
  
      FROM python:3.12
      WORKDIR /app
      RUN apt-get update && apt-get install -y curl && rm -rf /var/lib/apt/lists/*
      COPY requirements.txt .
      RUN pip install --no-cache-dir -r requirements.txt
      COPY . .
      HEALTHCHECK --interval=30s --timeout=5s --start-period=5s --retries=3 \
              CMD curl -f http://localhost:8000/health || exit 1
      CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
  - and pushed it on remote.
 
## Task 2: Reusable Workflow — Build & Test
- This workflow we made inorder to test our code with the help of pytest.

        name: first
        on:
          workflow_call:
            inputs:
              python_version:
                description: "This tells which interpretor to setup"
                type: string
                required: false
                default: 15
              run_tests:
                description: "This is an input to run tests"
                type: boolean
                default: true
        jobs:
          reuse:
            runs-on: ubuntu-latest
            steps:
              - name: code checkout
                uses: actions/checkout@v4
              - name: setup interpretor
                uses: actions/setup-python@v5
                with:
                  python_version: ${{ inputs.python_version }}
              - name: Install dependencies
                run: |
                  python -m pip install --upgrade pip
                  if [ -f requirements.txt ]; then
                    pip install -r requirements.txt
                    pip install pytest
                  fi
              - name: run tests
                if: ${{ inputs.run_tests }}
                run: pytest
  - This is not a standalone workflow this we will use in our main pipeline.
  - This triggers on workflow_call.
  - We have to use Inputs in workflow_call just like in for e.g python_version we have used default value which is version we will be using in this inputs desc,type,require and default can be constant.
  - Then we have created our jobs in which our first job is reuse which runs on  ubuntu-latest and has number of steps.
  - In first step we have used githubs very own action to checkout code actions/checkout@v4.
  - In next step we shall need an interpretor to run tests in this case is pur python setup.
  - for that also we have githubs own actions which is actions/setup-python@v5 to whom we informed to use our defined python_version in inputs using with.
  - Then we will install our requirements our dependencies on which we will run our tests.
     - In which we have first installed and upgraded pip
     - then with if/else condition we informed that if the requirements.txt file is available then pip install reuierments.txt and with it also install pytest.
     - and with fi we have closed the condition.
  - In the last step we have also used if with the input run_tests to run pytest which will read the boolean value from the input if true it will run if false it will skip.
  - Summary
      - This is a first and basic workflow which we will reuse in our main pipeline.
      - This will verify and check our code using pytest.
      - for this workflow below things we need to make sure.
          - code checkout
          - install interpretor
          - Install dependencies
          - Install the test prog.
##
