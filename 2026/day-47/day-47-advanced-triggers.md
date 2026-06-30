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

