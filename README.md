## Description
- Jenkins: Automated code compiles and conducts unit testing, triggering builds automatically upon Git changes.
- SonarQube: Integrated a code analysis tool, enforced code quality standards, and generated reports.
-	Nexus: Built an artifact repository and provided efficient storage, versioning, and dependency management.
-	Docker: Utilized application containerization, simplified deployment, and ensured consistency.
-	AWS ECR and ECS: Leveraged AWS ECR for Docker image storage and employed AWS ECS for reliable and scalable container deployment.
## Prerequisites
### AWS EC2
- Jenkins (Port 8080) using userdata/jenkins-setup.sh and add sonarqube security group in inbound rules at port 8080
- Nexus (Port 8081) using userdata/nexus-setup.sh and add jenkins security group in inbound rules at port 8081
- SonarQube (Port 80) using userdata/sonar-setup.sh and add jenkins security group in inbound rules at port 80
### AWS ECR
- Create a repository
### AWS ECS
- Create production and staging clusters
- Create task definition for both production and staging 
### Jenkins
- Install Maven Integration plugin
- Install Github Integration plugin
- Install Nexus Artifact Uploader plugin
- Install SonarQube Scanner plugin
- Install Slack Notification plugin
- Install Build Timestamp plugin
- Install Amazon ECR plugin
- Install CloudBees AWS Credentials Plugin
- Install java-1.8.0-openjdk-amd64 and used /usr/lib/jvm/java-1.8.0-openjdk-amd64 as JAVA_HOME
- Install maven 3
- At System/Slack, match workspace and channel in Slack and create a slack credential
- Create nexuslogin credential (username with password)
- Create sonartoken credential (secret text)
- Create applogin credential (ssh username with private key)
- Create nexuspass credential (secret text)
- Install Docker in Jenkins server
### Nexus
- Create maven2 (hosted) repository: project_name-release
- Create maven2 (proxy) repository: project_name-maven-central and enter url https://repo1.maven.org/maven2/ in Remote storage
- Create maven2 (hosted) repository: project_name-snapshot and change Version policy from Release to Snapshot
- Create maven2 (group) repository: project_name-maven-group and all repositories above
### SonarQube
- Create Quality Gates (Bugs is greater than 85)

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
