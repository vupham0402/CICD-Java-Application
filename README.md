## How to run
### Jenkins (StagePipeline)
- Make sure the names of repositories in Nexus match with names in the environment in Jenkinsfile
- Create a new item with Pipeline
- At Pipeline, choose Pipeline script from SCM -> Git -> ssh url -> create git credential -> select branch -> Jenkinsfile
- At Build Triggers, check mark GitHub hook trigger for GITScm polling
### SonarQube
- Add Quality Gates to the project after running the first time and run again
### Nexus
- Check project_name-release to see the artifact after building the Jenkins pipeline
### Github
- Create a webhook with public IP from Jenkins EC2 to automate building pipeline every new code is pushed to the branch
### AWS ECR
- Make sure the image is uploaded to the repository
### AWS ECS
- Check health and containers
