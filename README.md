My step-by-step Process of the project

STEP 1:
1. Unzip the given folder 
2. Create a Github repo with name "mean-devops-crud"
3. add all the frontend and backend folders to the github

STEP 2 :
1. Open cmd in the path of the folder on your local machine  
2. In AWS create a EC2 intsance with key pair 
3. by using Key pair connect your local machine with EC2 instance 
4. Run all the commnands in your local machine

STEP 3:
1. Install docker and login via local machine
2. Create a docker image  build and push it to the docker HUB

STEP 4:
1. Add the repective Dockerfile to both backend and frontend
2. using git commands commit and psuh these changes to github
3. Create a Docker compose file in main folder
4. Add and commit to github

STEP 5:
1. Using Docker compose command compose the yaml file
2. and open the app ui using public IP http://3.109.151.248
3. the app UI is displayed sucessfully and i have attached the screenshot of the app UI
4. Make sure edit the repected inbound rule HTTP PORT 80

STEP 6:
1. Install jenkins for CI/CD pipeline
2. After installing and updating the jenkins open it via port 8080
3. inside the jenkins install the required plugins
4. Create a new pipeline by usiing jenkins file
5. add that jenkins to GitHub
6. create a webhook in github repo and save all the changes
7. click on the "BUILD NOW" button
8. Sucessfully the CI/CD pipeline is built and the screenshot is attached to the repo

STEP 7:
1. install nginx by using command "nano nginx.conf"
2. add the required file and save it
3. Restart the container
4. open the url by "http://3.109.151.248"
