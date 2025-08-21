# Jenkins docker container for armv7 architectures (java 17)
1. Create a dockerfile with the following content:
```Dockerfile
FROM balenalib/raspberrypi3-debian:bullseye

RUN install_packages openjdk-17-jdk curl git
RUN curl -fsSL https://get.jenkins.io/war-stable/latest/jenkins.war -o /usr/share/jenkins.war
RUN mkdir -p /var/jenkins_home && chown -R root:root /var/jenkins_home

VOLUME /var/jenkins_home

EXPOSE 8080 50000

CMD ["java", "-jar", "/usr/share/jenkins.war"]
```
2. Build the docker image:
```
sudo docker build -t jenkins-armv7-jdk17 .
```
3. Execute the docker container:
```
sudo docker run -d \
  --name jenkins \
  -p 8080:8080 -p 50000:50000 \
  -v data:/var/jenkins_home \
  jenkins-armv7-jdk17
```
> [!NOTE]  
> Tested on a raspberry pi 400 and working perfectly

> [!TIP]  
> You should consider setting up a jenkins agent due to building in the built in node can have some security issues
