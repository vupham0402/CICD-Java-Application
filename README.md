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
### Nexus
- Create maven2 (hosted) repository: project_name-release
- Create maven2 (proxy) repository: project_name-maven-central and enter url https://repo1.maven.org/maven2/ in Remote storage
- Create maven2 (hosted) repository: project_name-snapshot and change Version policy from Release to Snapshot
- Create maven2 (group) repository: project_name-maven-group and all repositories above
### SonarQube
- Create Quality Gates (Bugs is greater than 85)
