FROM openjdk:11 AS BUILD_IMAGE
RUN apt update && apt install maven -y
RUN git clone -b cd-jenkins https://github.com/vupham0402/CICD_Java_Web_Application.git
WORKDIR /CICD_Java_Web_Application
RUN mvn -s pom.xml -DskipTests install

FROM tomcat:9-jre11

RUN rm -rf /usr/local/tomcat/webapps/*

COPY --from=BUILD_IMAGE CICD_Java_Web_Application/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war

EXPOSE 8080
CMD ["catalina.sh", "run"]
