# DevSecOps: Add Security to Your CI/CD Pipeline
## Devsecops
- Normally we use our code to build-test and deploy but devsecops is practice to apply test in each step to add more security instead of adding security in last step.
- This approach is also called as shift left approach.

## Trivy/dependecy scan
<img width="1710" height="711" alt="image" src="https://github.com/user-attachments/assets/953bcd7f-ceea-499f-8627-4b4248273e9b" />

- above image shows us where in the main pipeline we have used a trivy scanning which checks for vulnerabilities in pur images.
- we then have also used trivy in serif format.
- trivy basically scans our image checks for severities critical or high then as per our defined exit code it continues.
- then we upload our reports in paths and specific files which we also pass arguments in our trivy run.


<img width="1407" height="743" alt="pull request" src="https://github.com/user-attachments/assets/a14436d4-514b-4d62-80c4-6a313857b969" />

- This image shows us even before we run trivy we have used githubs own actions to check for any valnerabilities in our code.
- this we are doing even after we do pytest

## What I learned.
- We should use shift left approach.
- we should first check for dependcies in code.
- then also when the image is build we should do trivy scan which scans our vulnerabilities as well as scans for secrets.
- by this even if any secrets are leaked in our image before going in production we can detect them.
- we can transfer the results into txt or sarif files for more visibility of the data and take neccesary actions.
- Adding permissions is also very important which gives right to workflows to do changes like it shows us dependency scan results and to write files for us as artifacts.
