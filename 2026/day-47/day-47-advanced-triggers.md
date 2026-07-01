# Advanced Triggers: PR Events, Cron Schedules & Event-Driven Pipelines
## Task 1: Pull Request Event Types
<img width="1014" height="582" alt="image" src="https://github.com/user-attachments/assets/b51d8a1f-9932-436b-befe-c0a7bf1490dc" />
<img width="748" height="429" alt="image" src="https://github.com/user-attachments/assets/14932727-c69f-4603-a6c4-3cb0ce6ba834" />
<img width="866" height="490" alt="image" src="https://github.com/user-attachments/assets/500c6e43-05c9-48c1-b6e1-172bdb0a46ac" />

- In this we tested different events related to pull_request.
- earlier we tested that if pull_request is created the pipeline gets triggered.
- But in this we saw other types like open closed on which oue pipe line got triggered and also gave us desired outputs.
  
## Task 2: PR Validation Workflow
- This is a yaml file which triggers on pull request on main.
- in first job checks file size
- second checks branch name if feature/something will pass otherwise fails as in below snap
- third is where it gives warning if the body is empty
  
 <img width="1680" height="977" alt="image" src="https://github.com/user-attachments/assets/59cff6fa-805e-4c20-91c0-a9e71d9410e6" />
  
 <img width="1164" height="552" alt="image" src="https://github.com/user-attachments/assets/920a1b0c-136a-41b5-ba2c-3d105dd462ae" />
 <img width="1147" height="578" alt="image" src="https://github.com/user-attachments/assets/237c693c-9be6-4e53-a97d-6ea8e9a6b078" />

## Task 3: Scheduled Workflows (Cron Deep Dive)

<img width="1230" height="554" alt="image" src="https://github.com/user-attachments/assets/038d6eba-a22d-4ef8-abea-690a96ce01c2" />



- In above workflow we have scheduled cron job basically two jobs one which which should have triggered.
- github actions workflows are not guranteed to trigger on time they during high load they can be delayed.
- The cron expression for: every weekday at 9 AM IST
    - cron: ''30 3 * * *'


## Task 4: Path & Branch Filters

<img width="772" height="439" alt="image" src="https://github.com/user-attachments/assets/ea73064a-a31f-4aa6-8c5c-e148103580b9" />

- this basically is triggered when files in mentioned path changed.
- in above example earlier when i pushed with no changes it did not triggered.
- but as i changed on of the mentioned files it got triggered.
- also we can use 'paths-igonre' this will do not trigger if the changes are made in listed files to ignore.

## Task 5: workflow_run — Chain Workflows Together
- just like we use needs to create dependency of one job onto another.
- we use workflow_run: workflows: types to only run the workflow when the mentioned workflow in this is successful.
  
<img width="680" height="388" alt="image" src="https://github.com/user-attachments/assets/24d7913f-b134-4dfc-a9fd-df74cd2788ab" />


<img width="783" height="448" alt="image" src="https://github.com/user-attachments/assets/65959ebb-8e04-41ab-b573-9135fd069519" />

## Task 6: repository_dispatch — External Event Triggers
- This is the workflow which gets triggered not by any event on github but externall event.
- in below example we pushed a workflow on github which includes on:repository_dispatch:types: and in our shell we have github loggein from there we un gh post which triggered our workflow.
- here our shell acts as external system.

<img width="807" height="353" alt="image" src="https://github.com/user-attachments/assets/c1c0aaa9-5893-42ad-b6a5-d03a4165e7df" />

