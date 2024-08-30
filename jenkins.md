# CI / CD Pipeline Using Jenkins
## Different Enviornments

1. Dev Envionment
   - Development Process  

2. QA
   - Quality Assurance Env. Or Testing Env

3. UAT
   - User Acceptance Testing   

4. Pilot Env (Pre Prod Env)
    - Performance Test     

5. Production Env
    - Live the Application     

## What is CI/CD

**Continuous Integration** - 
is an automation to build and test application whenever new commits are pushed into the branch.

**Continuous Delivery** -
is Continuous Integration + Deploy application to production by "clicking on a button" (Release to customers is often, but on demand).

**Continuos Deployemnt** - 
is Continuous Delivery but without human intervention (Release to customers is on-going).

![CI/Cd](https://i.sstatic.net/vEULO.png)

## Steps to Install Tomcat & Jenkins On Aws

First we have to update the dependencies
>sudo apt update

After this to run tomcat we need java, so install java
>sudo apt install openjdk-17-jdk

**Install Tomcat**
[Install tomcat reference](https://www.linkedin.com/pulse/how-install-configure-tomcat-9-ubuntu-voleti-lavanya-if5ge)

To configure the systemctl command setup the .service file
~~~
sudo nano /etc/systemd/system/tomcat.service

[Unit]
Description=Apache Tomcat Web Application Container
After=network.target

[Service]
Type=forking

Environment=JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-amd64/jre
Environment=CATALINA_PID=/opt/tomcat/temp/tomcat.pid
Environment=CATALINA_Home=/opt/tomcat
Environment=CATALINA_BASE=/opt/tomcat
Environment=’CATALINA_OPTS=-Xms512M -Xmx1024M -server -XX:+UseParallelGC’
Environment=’JAVA_OPTS.awt.headless=true -Djava.security.egd=file:/dev/v/urandom’

ExecStart=/opt/tomcat/bin/startup.sh
ExecStop=/opt/tomcat/bin/shutdown.sh

User=tomcat
Group=tomcat
UMask=0007
RestartSec=10
Restart=always

[Install]

WantedBy=multi-user.target
~~~

**Install Jenkins**
~~~
sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]" \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins
~~~
