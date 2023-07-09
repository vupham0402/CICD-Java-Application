## Prerequisites
### AWS EC2
- Jenkins (Port 8080) using userdata/jenkins-setup.sh and add sonarqube security group in inbound rules at port 8080
- Nexus (Port 8081) using userdata/nexus-setup.sh and add jenkins security group in inbound rules at port 8081
- SonarQube (Port 80) using userdata/sonar-setup.sh and add jenkins security group in inbound rules at port 80
- app01-staging (Port 8080) and add jenkins security group in inbound rules at port 22
### Route 53
- Create a hosted zone (private hosted zone)
- Create a record and add app01-staging private ip into value
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
- Install Ansible in Jenkins server
- Install Ansible plugin
### Nexus
- Create maven2 (hosted) repository: project_name-release
- Create maven2 (proxy) repository: project_name-maven-central and enter url https://repo1.maven.org/maven2/ in Remote storage
- Create maven2 (hosted) repository: project_name-snapshot and change Version policy from Release to Snapshot
- Create maven2 (group) repository: project_name-maven-group and all repositories above
### SonarQube
- Create Quality Gates (Bugs is greater than 85)

## How to run
### Jenkins 
- Make sure the names of repositories in Nexus match with names in the environment in Jenkinsfile
- Make sure the name of records in Route 53 match in stage.inventory file
- Create a new item with Pipeline
- At Pipeline, choose Pipeline script from SCM -> Git -> ssh url -> create git credential -> select branch -> Jenkinsfile
- At Build Triggers, check mark GitHub hook trigger for GITScm polling
### SonarQube
- Add Quality Gates to the project after running the first time and run again
### Nexus
- Check project_name-release to see the artifact after building the Jenkins pipeline
### Github
- Create a webhook with public IP from Jenkins EC2 to automate building pipeline every new code is pushed to the branch

