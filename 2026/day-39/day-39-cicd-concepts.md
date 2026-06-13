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
  a devloper pushed the code the automated CI triggers which first peroforms linting where we check the sytanx errors in our code,
  then we build our code into a reusable artifact which then gets tested if successful the artifact gets pushed to registry such as docker hub.
  If the test fails the build stage is marked as failed.

- how often
  Every time a devloper pushes the code into main/master branch the CI gets triggered.

- what it catches
  It basically compiles our code runs linting tests to check for syntax error in our code.
  After the build stage it again tests our artifacts if failed it notifies us.

  ### Continuous Delivery — how it's different from CI, what "delivery" means
