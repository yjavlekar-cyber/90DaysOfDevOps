# Docker Build & Push in GitHub Actions
- This is CI/CD pipeline for a simple resturant website.
- This pipeline is triggered with push on main branch.
  
      name: shriwardhan
      on:
        push:
          branches: [ "main" ]
- Under jobs we have two jobs first job builds the image and pushes it to docker hub and second job deploys the same image on selh-hosted runner which is our laptop.
- 1) build_and_push:
     - 1) we have first decided on which os it shall run in this case it is ubuntu.
          
              runs-on: ubuntu-latest

       2) Then checksout the code from the repository.
       3) builds our images
       4) logins to dockerhub using our username and password which are stored as variable and secrets.
       5) Then tags and pushes this image on registry in this case which dockerhub.
      
              steps:
                #code checkout will analyze our repository.
                - name: Code checkout
                  uses: actions/checkout@v4
          
                #This will build the image from our dockerfile.
                - name: build image(front)
                  run: docker build -t shri-frontend ./shri-tour/frontend
          
                - name: build image(backend)
                  run: docker build -t shri-backend ./shri-tour/backend
          
                #This will login docker hub.
                - name: login to docker hub
                  uses: docker/login-action@v3
                  with:
                    username: ${{ vars.USERNAME }}
                    password: ${{ secrets.PASSWORD }}
          
                #This will tag and push the images on dockerhub.
                - name: docker tag and push frontend
                  if: github.ref == 'refs/heads/main'
                  run: |
                    docker tag shri-frontend ${{ vars.USERNAME }}/shri-frontend:latest
                    docker tag shri-frontend ${{ vars.USERNAME }}/shri-frontend:${{ github.sha }}
                    docker push ${{ vars.USERNAME }}/shri-frontend:latest
          
                - name: docker tag and push backend
                  if: github.ref == 'refs/heads/main'
                  run: |
                    docker tag shri-backend ${{ vars.USERNAME }}/shri-backend:latest
                    docker tag shri-backend ${{ vars.USERNAME }}/shri-backend:${{ github.sha }}
                    docker push ${{ vars.USERNAME }}/shri-backend:latest
- 2) deploy_on_github:
     - 1) This job needs our build_and_push job to succeed to run.
       2) It runs-on self-hosted runner which is already saved in our github.
       3) Then checksout the code using actions.
       4) using docker pull we pull the image from registry.
       5) we stopped old containers.
       6) then using the docker-compose up -d we generated new containers which runs on our local laptop.
      
           deploy_on_github: #this is job2
    runs-on: self-hosted #this job will run on self-hosted run which is our laptop as of now
    needs: build_and_push

              steps:
                - name: Code checkout
                  uses: actions/checkout@v4
          
                #This will pull the image
                - name: pull latest image(front)
                  run: docker pull ${{ vars.USERNAME }}/shri-frontend:latest
          
                - name: pull latest image(backend)
                  run: docker pull ${{ vars.USERNAME }}/shri-backend:latest
          
                #This will stop any old containers.
                - name: stop old containers
                  run: docker compose down || true
          
                #This will start new containers.
                - name: start new containers
                  run: docker compose up -d
                  env:
                    DOCKER_USERNAME: ${{ vars.USERNAME }}


- 
   # | Issue                                                                                                                     | Fix
  ---|---------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------
   1 | 3 syntax errors — Job 2 used  uses:  instead of  run:  for docker pull, backend tag used  secrets.PASSWORD  instead of    | Changed  uses:  →  run: , fixed variable references, added  needs
     | vars.USERNAME , and Job 2 missing  needs: build_and_push                                                                  |
   2 | Username in secrets — Docker Hub username was stored in  secrets  instead of  vars , so  ${{ vars.USERNAME }}  was empty  | Moved username to repository variables ( vars.USERNAME )
   3 | Invalid docker tag — Backend tag step still used  secrets.PASSWORD astheimagename                                         | Changedto {{ vars.USERNAME }}
   4 | docker-compose.yml not found — Job 2 (self-hosted runner) had no  actions/checkout@v4 , so no repo files were available   | Added  actions/checkout@v4  step in Job 2
   5 | Invalid reference format in compose —  docker-compose.yml  used  vars.USERNAME                                            | Changedto {DOCKER_USERNAME}  and passed it via  env:  in the workflow step
     | (GitHubActionssyntax)whichdoesn'tworkinsidecomposefiles,plusbackendimageagainusedPASSWORD                                 |

                 
