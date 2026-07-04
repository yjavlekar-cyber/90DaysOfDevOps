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
            
## Task 3: Reusable Workflow — Docker Build & Push
- This again is a reusable workflow which we will use in our main pipeline.
- purpose of this workflow is to build our docker image using our pushed dockerfile and pushed the final image to dockerhub which is our image registry.
  
          name: second
          on:
            workflow_call:
              inputs:
                image:
                  description: "image name"
                  required: false
                  type: string
                  default: my-app
                tag:
                  description: "image-tag"
                  default: latest
                  type: string
          
              secrets:
                docker_username:
                  required: true
                docker_token:
                  required: true
          
              outputs:
                my-outputs:
                  value: ${{ jobs.reuse-sec.outputs.my_job_output }}
          jobs:
            reuse-sec:
              runs-on: ubuntu-latest
              outputs:
                my_job_output: ${{ steps.image.outputs.image_url }}
          
              steps:
                - name: code checkout
                  uses: actions/checkout@v4
                - name: docker login and build
                  uses: docker/login-action@v3
                  with:
                    username: ${{ secrets.docker_username }}
                    password: ${{ secrets.docker_token }}
                - name: docker build
                  run: |
                    docker build -t ${{ inputs.image }} .
                    docker tag ${{ inputs.image }} ${{ secrets.docker_username }}/${{ inputs.image }}:${{ inputs.tag }}
                    docker push ${{ secrets.docker_username }}/${{ inputs.image }}:${{ inputs.tag }}
                - name: set image output 
                  id: image
                  run: echo "image_url=docker.io/${{ inputs.image }}:${{ inputs.tag }}" >> "$GITHUB_OUTPUT"

- This workflow again uses workflow_call wherein our inputs are our image name and image tag.
- Then with inputs we have also assigned secrets whos value we will derive or mention in main pipeline and that value this secrets will use to apply in this current workflow.
- Then we have also assigned outputs whos input will be used by main-pipeline
    - First we have top level output which points towards jobs then a specific job called reuse and its outputs with the name my_job_outputs.
    - Under job level output we have used steps and a specific step id-image then its outputs from image_url
    - in that step we have passed our output into $GITHUB_OUTPUTS whose value is used by outputs.
- We then have jobs with the name reuse-sec which runs on ubuntu-latest and has outputs as explained in earlier step.
- as usual our first step is to checkout the code/repo
- then with githubs own action to login github docker/login-action@v3 with the username and password which we have mentione in inputs we have logged in into dockerhub.
- Then next builds,tags and pushes our image to docker hub.
- then last step forwards the image name into variable image_url whos value is then passed into $GITHUB_OUTPUTS which is used by earlier outputs.

## Task 5: Main Branch Pipeline
This is a main branch pipeline which uses our earlier two workflows runs them and also runs vulnerability check on our image.

    name: main
        on:
          push:
            branches: [ "main" ]
        jobs:
          first:
            uses: ./.github/workflows/reusable-build-test.yml
          second:
            needs: first
            uses: ./.github/workflows/docker-reusable.yml
            with:
              image: my-app
              tag: latest
            secrets:
                docker_username: ${{ secrets.DOCKER_USERNAME }}
                docker_token: ${{ secrets.DOCKER_TOKEN }}
          deploy:
            runs-on: ubuntu-latest
            needs: second
            environment: production
            env:
              node: --trace-deprecation
            steps:
              - name: Image deploying to prodcution
                env:
                  image: ${{ needs.second.outputs.my-outputs }}
                run: echo "Deploying image- $image to production"
              - name: login to docker
                uses: docker/login-action@v3
                with:
                  username: ${{ secrets.docker_username }}
                  password: ${{ secrets.docker_token }}
              - name: Run trivy vulenrabilities
                id: view
                uses: aquasecurity/trivy-action@v0.36.0
                with:
                  image-ref: '${{ secrets.DOCKER_USERNAME }}/my-app:latest'
                  format: 'table'
                  output: 'trivy.txt'
                  severity: 'CRITICAL,HIGH'
                  exit-code: '1'
              - name: upload this to report
                uses: actions/upload-artifact@v4
                with:
                  name: trivy-report
                  path: trivy.txt
- This workflow with name main triggers when pushed to main branch.
- Then under jobs our fist job uses path of our first workflow which tests our code with the keyword uses.
- In second job we have used our second workflow which builds,tags and pushes our image and which also needs our first workflow to run then this workflow will run.
    - under uses we have mentioned image and tag under with these values we have mentioned as inputs in our reusable workflow.
    - after that we have mentioned our secrets from reusable workflow and gave the secrets which are saved in github actions.
- We have our third job called deploy which runs on ubuntu and needs second workflow to run and which uses env as production.
- under depoloy we have first step which prints the image name using the outputs from our previous workflows.
- Then we need to scan vulnerabilities
    - where first we will login to our docker using githubs own action.
    - then after this step in another step we will use trivy to scan our image using argumenyts like with -image-ref(image name),severity,exit-code etc
    - then in last step we have transfered the report from this scan into a file using githubs own action for this.
- to skip the trviy version we will create trivy.yaml which will have this skip config and we will mention it as argument under trivy scanning as trivy-config.
- also the file mentioned in last step we will also mention that file in the arguments followed whil scanning as outputs: file.

## Running Container
Once our main-pipeline is successful we will use this workflow to run our containers for this image.

      name: deployin_in_container
         on:
          workflow_dispatch:  
        jobs:
          cont:
            runs-on: ubuntu-latest
            steps:
            - name: pull image
              run: docker pull yjawlekar/my-app:latest
            - name: run
              run: docker run -d --name my-container -p 8000:8000 yjawlekar/my-app:latest
            - name: debug container state
              run: |
                echo "--- docker ps ---"
                docker ps -a
                echo "--- docker logs ---"
                docker logs my-container
            - name: wait for container
              run: sleep 15
            - name: health check
              id: health
              run: |
                if curl -s -f http://localhost:8000/health > /dev/null ; then
                  echo "Status=PASSED" >> $GITHUB_OUTPUT
                  echo "Health check PASSED"
                else
                  echo "Status=FAILED" >> $GITHUB_OUTPUT
                  echo "Health check FAILED"
                fi
            - name: stop and remove
              if: always ()
              run: |
                docker stop my-container || true
                docker rm my-container || true
            - name: write summary
              if: always ()
              run: |
                echo "## Health Check Report" >> $GITHUB_STEP_SUMMARY
                echo "- Image: myapp:latest" >> $GITHUB_STEP_SUMMARY
                echo "status:${{ steps.health.outputs.status }}" >> $GITHUB_STEP_SUMMARY
                echo "- Time: $(date)" >> $GITHUB_STEP_SUMMARY
            - name: fail job if unhealthy
              if: steps.health.outputs.status == 'Failed'
              run: exit 1
- In this workflow the trigger that we have used is workflow_dispatch which will not be triggered automatically but needs our manual intervention to start.
- Then we have defined jobs under which our job which runs on ubuntu-latest
- the first step pulls image from dockerhub.
- then runs the container with port with specific name and our pulled image
- then in next step we we have fetched our docker all containers and its logs to inspect.
- In next step by running sleep 15 we will wait 15sec for container to start.
- Then we did health check step which curls our local host passes status into $GITHUB_OUTPUT if passed or failed.
- then in second last step we will stop and remove all the old containers before running this containers.
- then using $GITHUB_STEP_SUMMARY we are printing our image name,time and whatever the status is using outputs passed in healt check step.
- and if the the value from outputs is failed we asked our script to run exit 1 that means our workflow will return exit code 1.
  
## # CI/CD Lessons Learned — Quick Reference

1. **`git remote add origin <url>`** for the first-ever remote link — use `set-url` only when *changing* an existing one.

2. **Secret and variable names are case-sensitive and scope-limited.** A secret passed into a reusable workflow's inputs doesn't automatically exist in other sibling jobs — reference the real repo secret (usually UPPERCASE) directly in each job that needs it.

3. **Action input keys must match exactly** (e.g. `python-version`, not `python_version`). A wrong key name fails silently — no error, just ignored — so double-check against the action's docs.

4. **Prefer `-slim` (or alpine) base images** over full images. Smaller base = fewer OS packages = fewer vulnerabilities to scan and patch.

5. **A scanner "failing" your pipeline is often correct, not broken.** If you set `exit-code: 1` on CRITICAL/HIGH findings, a real vulnerability should stop the pipeline — that's the tool doing its job.

6. **Keep container/resource names consistent across every step** in a workflow (create, inspect, stop, remove) — a name typo in one step breaks that step silently.

7. **Match string values exactly, including case**, when comparing step outputs (`'FAILED' == 'FAILED'`, not `'FAILED' == 'Failed'`) — otherwise conditional checks silently never trigger.

8. **Always add `if: always()`** to cleanup/reporting steps so they still run even when an earlier step in the same job fails.

9. **Test the exact endpoint your infrastructure depends on.** If your health check hits `/health`, make sure a test explicitly covers `/health` — not just the root route — so a broken health check is caught early, not in production.

10. **When copy-pasting/editing YAML by hand, re-view the whole file before running it.** Indentation slips and merged lines (e.g. a step accidentally appended to the previous step's `run:` block) are invisible in a quick skim but break the entire workflow.






                                     
