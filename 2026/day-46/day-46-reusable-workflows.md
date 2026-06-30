# Reusable Workflows & Composite Actions
## Task 1: Understand workflow_call
  - What is a reusable workflow?
    Reusable workflow is just like normal workflow that we create in .github/workflows which can be then reused by any other workflow just by calling it.

  - What is the workflow_call trigger?
    Whenever we want a workflow to be reused any where we can use workflow_call in script.

  - How is calling a reusable workflow different from using a regular action (uses:)
    when we use a whole workflow it basically contains whole purpose of that workflow but when we use regular action it just using earlier action in that same script.

  - Where must a reusable workflow file live?
    reusable workflow should live inside our repo's .github/workflows.

## Task 2: Create Your First Reusable Workflow
- This is a reusable workflow which we will call in another workflow.
- This we define by using workflow_call.
- This prints from input and environment.
- and also checks if docker token available or not.

      name: reuse
      on:
        workflow_call:
          inputs:
            app_name:
              description: "new-app"
              type: string
              required: true
            environment:
              type: string
              required: true
              default: staging
          secrets:
            docker_token:
                  required: true
      
      jobs:
        rreuse:
          runs-on: ubuntu-latest
          steps:
            - name: code checkout
              uses: actions/checkout@v4
            - name: prints
              run: echo "Building ${{ inputs.app_name }} for ${{ inputs.environment }}"
       - name: Check docker token status
              run: |
                if [ -n "${{ secrets.docker_token }}" ];then
                  echo "Docker token is set: true"
                else
                  echo "Docker token is set: false"
                fi
  ## Task 3: Create a Caller Workflow
- This is a caller workflow which gets triggered when pushed on main.
- in jobs it simply uses the path to our reusable workflow.
- In this we have defined the app_name,environment and our secrets docker_token
- when we push this the jobs in reusable where we have asked to print they use the inputs and environments and secrets declared in caller job.
  <img width="1263" height="535" alt="image" src="https://github.com/user-attachments/assets/39abaa49-024b-4a8f-b154-5de64f14b4b4" />

        name: caller
        on:
          push:
            branches: [ "main" ]
        jobs:
          token:
            uses: ./.github/workflows/reusable-build.yml
            with:
              app_name: "my-web-app"
              environment: "production"
            secrets:
              docker_token: ${{ secrets.DOCKER_TOKEN }}

## Task 4: Add Outputs to the Reusable Workflow
<img width="1079" height="1023" alt="image" src="https://github.com/user-attachments/assets/6a8fe6f4-c980-4578-9c48-be5d19294e9f" />

In this workflow:(reusable)
- we have one top level output which acts first outside the job inside values.
- then we have a job inside the actual job.
- 

<img width="968" height="581" alt="image" src="https://github.com/user-attachments/assets/982065f8-aebe-4720-b566-863fce0802bd" />
In this caller workflow:
- we have used the output inside the steps.

- This both workflows are different but we have connected the first workflow with second one using workflow_call in first and the path of the same is used by caller workflow inside it.
  
<img width="715" height="421" alt="image" src="https://github.com/user-attachments/assets/45b39771-e9e8-4353-8a74-65058a8d3e0e" />

- In this common mistakes i made were of spellings,hyphens then sequence where in job needs should have been used first then runs-on.

## Task 5: Create a Composite Action
<img width="1071" height="814" alt="image" src="https://github.com/user-attachments/assets/708e40e1-8bdf-47b1-9693-418cc670a4dc" />

- This is a workflow saved in different folder in .github.
- In this we dont have to declare jobs we just need to use runs: using: composite.
- In this we have used outputs directly from steps
- the outputs from steps gets store in the outputs: greeted:
  
<img width="1247" height="615" alt="image" src="https://github.com/user-attachments/assets/a0a08d06-08bd-4af5-81f9-e0df56bda568" />

- This is where we have called our composite workflow.
- after checkout we need to mention id and path of our compiste workflow.
- In this we have used the stored output in outputs:greeted: in steps.greeting.outputs.greeted
- several mistakes:
    - naming mismatch
    - hyphen mismatch
    - double qoutes missing
    - indentation missing
 
# Task 6: Reusable Workflow vs Composite Action

| | Reusable Workflow | Composite Action |
|---|---|---|
| **Triggered by** | `workflow_call` | `uses:` in a step |
| **Can contain jobs?** | Yes — one or more jobs, each with its own `runs-on` | No — no job layer at all, just a `steps:` list |
| **Can contain multiple steps?** | Yes, within each job | Yes — that's its only structure |
| **Lives where?** | A separate workflow YAML file under `.github/workflows/` | A folder with `action.yml` (or `.yaml`) under `.github/actions/<name>/` (or a separate repo) |
| **Can accept secrets directly?** | Yes — has a dedicated `secrets:` block in `workflow_call` and the caller passes them explicitly | No — secrets aren't passed in directly; it inherits whatever environment/secrets the calling job already has access to |
| **Best for** | Sharing entire job/workflow logic (multiple jobs, `runs-on`, matrix builds, multi-job pipelines) across workflows or repos | Sharing a reusable sequence of steps within a single job (e.g. setup, greeting, common shell logic) |

## Key takeaway
A reusable workflow is essentially a callable *workflow* (jobs and all), while a composite action is a callable *set of steps* that gets inlined into whatever job calls it — there's no job boundary inside a composite action.
