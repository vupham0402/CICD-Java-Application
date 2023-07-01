# CICD-Jenkins-Nexus-SonarQube
 
## Prerequisites
### AWS EC2
- Jenkins using userdata/jenkins-setup.sh
- Nexus using userdata/nexus-setup.sh
- SonarQube using userdata/sonar-setup.sh
### Jenkins
- Install Maven Integration plugin
- Install Github Integration plugin
- Install Nexus Artifact Uploader plugin
- Install SonarQube Scanner plugin
- Install Slack Notification plugin
- Install Build Timestamp plugin
- Install java-1.8.0-openjdk-amd64 and used /usr/lib/jvm/java-1.8.0-openjdk-amd64 as JAVA_HOME
- Install maven 3
### Nexus
- Create maven2 (hosted) repository: project_name-release
- Create maven2 (proxy) repository: project_name-maven-central and enter url https://repo1.maven.org/maven2/ in Remote storage
- Create maven2 (hosted) repository: project_name-snapshot and change Version policy from Release to Snapshot
- Create maven2 (group) repository: project_name-maven-group and all repositories above
### SonarQube
- Create Quality Gates (Bugs is greater than 85)
