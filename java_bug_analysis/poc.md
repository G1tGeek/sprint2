# Bugs Analysis : Proof of Concept

![image](https://github.com/user-attachments/assets/e065c14b-f67c-4cc4-ac3f-15d07034cf99)


## Author
|  Version   |   Author     |  Modifed   |      Comment      |    Reviewer      |
|------------|--------------|------------|-------------------|------------------|
|  V1        | Yuvraj Singh |            | Internal Review   | Siddharth Pawar  |
|  V2        | Yuvraj Singh |            | L0 Review         | Naveen Haswani |
|  V3        | Yuvraj Singh |            | L1 Review         | Deepak Nishad |
|  V4        | Yuvraj Singh |            | L2 Review         | Ashwani Singh |

## Table of Contents

<details>
<summary>1. Introduction</summary>

- [Introduction](#introduction)  
- [What and Why Bug Analysis?](#what-and-why-bug-analysis)  

</details>

<details>
<summary>2. Steps of Conduct</summary>

- [Prerequisites](#prerequisites)
- [Install Dependencies](#install-dependencies)
- [Configuration](#configuration)
- [Service for SonarQube](#service-for-sonarqube)
- [Testing the API](#testing-the-api)

</details>

<details>
<summary>3. Wrap-up</summary>

- [Conclusion](#conclusion)  
- [Contact Information](#contact-information)  
- [References](#references)  

</details>


## Introduction
This document offers a straightforward guide to identifying and addressing bugs in Java code. Implementing systematic bug analysis ensures that developers detect issues early, improve code reliability, and maintain application performance and security.

## What and Why Bug Analysis?

To get a detailed about bug analysis in java [click here]().

## Steps of Conduct

### Prerequisites

| Dependency   | Minimum Version |
| ------------ | --------------- |
| Operating System | Ubuntu 22.04 |
| CPU    | 2 vCPU  |
| Hard Disk   | 25 GB  |
| RAM           | 4 GB     |
| Java JDK     | 17+             |
| PostgreSQL   | Latest Stable   |
| unzip        | Latest Stable   |
| SonarQube    | Latest Stable   |
| SonarScanner | Any Version   |
| Maven        | 3.6+            |
| SonarQube | 9000 (open)        |
| Secure HTTPS web traffic | 443  |       
| PostgreSQL database access | 5432  | 


### Install Dependencies

  *[Go to this link](https://github.com/snaatak-Downtime-Crew/Documentation/blob/main/common_stack/operating_system/ubuntu/sop/commoncommands/README.md#1-basic-system-commands) and follow `STEP 3. Update and Upgrade Packages`.*
  
  ![image](https://github.com/user-attachments/assets/436278c3-993e-48e5-912d-01a07aed633e)

- **Install Java**

  *[Go to this link](https://github.com/snaatak-Downtime-Crew/Documentation/tree/main/common_stack/application/java/installation/guide#java-installation-steps-ubuntu) and follow `Java Installation Steps (Ubuntu)`.*
  
  ![image](https://github.com/user-attachments/assets/6bf62845-fe4d-4729-9262-eabd824893fa)

- **Install PostgreSQL**

  *[Go to this link](https://github.com/snaatak-Downtime-Crew/Documentation/tree/main/common_stack/software/postgresql/installation#step-by-step-setup-guide) and follow `Step-by-Step Setup Guide` upto step 3.*
  
  ![image](https://github.com/user-attachments/assets/f9a86130-61d8-4bb2-8592-f5991ffe24c2)


- **Install unzip**

  *[Go to this link](https://github.com/snaatak-Downtime-Crew/Documentation/tree/main/common_stack/operating_system/ubuntu/sop/softwaremanagement#3-Install-a-Software) and follow `3. Install a Software` Package name: unzip*
  
  ![image](https://github.com/user-attachments/assets/5816daf7-40d3-4094-9aa4-450d1f531782)

- **Install SonarQube**

  ```
  sudo wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-9.9.3.79811.zip
  sudo unzip sonarqube-9.9.3.79811.zip
  sudo mv sonarqube-9.9.3.79811 /opt/sonarqube
  sudo groupadd sonar
  sudo useradd -d /opt/sonarqube -g sonar sonar
  sudo chown sonar:sonar /opt/sonarqube -R
  ```

  ![image](https://github.com/user-attachments/assets/4392851d-7266-4b04-b1cb-566618138d65)

- **Install SonarScanner**

  ```
  cd /opt
  sudo wget "https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-7.1.0.4889-linux-x64.zip" -O sonar-scanner.zip
  sudo unzip sonar-scanner.zip
  sudo mv sonar-scanner-7.1.0.4889-linux-x64 sonar-scanner
  sudo chown -R $USER:$USER sonar
  echo "export PATH=$PATH:/opt/sonar-scanner/bin" >> ~/.bashrc
  source ~/.bashrc
  ```

  ![image](https://github.com/user-attachments/assets/e863f3f2-770d-41d6-908f-8374f905f610)

- **Install Maven**

  *Install Maven* [Go to this link](https://github.com/snaatak-Downtime-Crew/Documentation/blob/main/common_stack/application/java/maven/sop/README.md#step-2-install-maven-and-check-version) and follow `Step 2: Install Maven and check version`.

  ![image](https://github.com/user-attachments/assets/149474b7-83b8-4ddb-8947-acf3497309f8)

### Configuration

- **PostgreSQL**-

  > *Change postgre default password*

  ```
  sudo passwd postgres
  ```

  ![image](https://github.com/user-attachments/assets/cc531230-3c86-4616-b664-e1ace5e2fbeb)

  > *Access postgre user*

  ```
  sudo - postgres
  ```

  ![image](https://github.com/user-attachments/assets/4e13ff74-6e2f-4cc9-8cbf-54c36a3500e4)

  > *Create a user sonar*

  ```
  createuser sonar
  ```

  ![image](https://github.com/user-attachments/assets/57a7c771-e5bb-4aea-9b18-612f7f5d302e)

  > *Log in to PostgreSQL and create database*

  ```
  psql
  
  ALTER USER sonar WITH ENCRYPTED PASSWORD 'sonar';
  CREATE DATABASE sonarqube OWNER sonar;
  GRANT ALL PRIVILEGES ON DATABASE sonarqube to sonar;
  ```
  
  ![image](https://github.com/user-attachments/assets/6304fe01-5ba1-4f71-88c0-8f596c267655)

  > *Quit*
  
  ```
  \q
  exit
  ```

  ![image](https://github.com/user-attachments/assets/4d8c2532-d319-4451-b03c-0ce0c5f6870d)

- **SonarQube**

  > *Edit the configuration file at `/opt/sonarqube/conf/sonar.properties` and add these database settings`*
  
  ```
  sonar.jdbc.username=sonar
  sonar.jdbc.password=sonar
  sonar.jdbc.url=jdbc:postgresql://localhost:5432/sonarqube
  ```

  ![image](https://github.com/user-attachments/assets/701c59e6-65c7-4a3c-a240-4e1a1a2ed989)

  > *Modify Kernel System Limits at `/etc/sysctl.conf`*
    ```
    vm.max_map_count=262144
    fs.file-max=65536
    ulimit -n 131072
    ulimit -u 8192
    ```

    ![image](https://github.com/user-attachments/assets/1f901c3c-5994-4c9f-9a29-91d78aec6c35)

  > *Reboot the system to apply the changes*
  ```
  sudo reboot
  ```

- **SonarScanner**

  > *Edit the configuration file at `/opt/sonar-scanner/conf/sonar-scanner.properties` and add your SonarQube server URL*

  ```
  sonar.host.url=http://localhost:9000
  ```

  ![image](https://github.com/user-attachments/assets/37dc2953-8948-4b2e-9361-d57f892e43d6)


### Service for SonarQube

*Create a file at `/etc/systemd/system/sonarqube.service` and add the below block*

```
[Unit]
Description=SonarQube service
After=syslog.target network.target

[Service]
Type=forking
User=sonar
Group=sonar
ExecStart=/opt/sonarqube/bin/linux-x86-64/sonar.sh start
ExecStop=/opt/sonarqube/bin/linux-x86-64/sonar.sh stop
StandardOutput=journal
LimitNOFILE=131072
LimitNPROC=8192
TimeoutStartSec=5
Restart=always
SuccessExitStatus=143

[Install]
WantedBy=multi-user.target
```

*Start the server*

```
sudo systemctl daemon-reload
sudo systemctl start sonarqube
sudo systemctl enable sonarqube
```

![image](https://github.com/user-attachments/assets/5aaef7c9-740d-4505-8094-8459f5d66fb6)

### Testing the API  

*Clone your [Salary API](https://github.com/OT-MICROSERVICES/salary-api.git) project repository from GitHub*

![image](https://github.com/user-attachments/assets/21c5c5ae-14d0-4d86-b769-8f5e47a305a8)


- **Start SonarQube Server**  

 > *Go-to SonarQube server at `<public-ip>:9000`*

  ![image](https://github.com/user-attachments/assets/ab8a3843-75d8-42de-96da-033bc5658014)

- **Generate SonarQube Authentication Token**  

 > *Create an authentication token for scanning. `My Account > Security`*

 ![image](https://github.com/user-attachments/assets/33f5a2ab-b581-4532-a846-f211dbff1137)

- **Configure the Project for SonarQube**

 > *Add SonarQube plugin configuration to Salary-API pom.xml.*
 
 ```
 <plugin>
      <groupId>org.sonarsource.scanner.maven</groupId>
      <artifactId>sonar-maven-plugin</artifactId>
      <version>3.9.1.2184</version>
 </plugin>
 ```

 ![image](https://github.com/user-attachments/assets/f4f27777-aefc-422f-a8ac-a881611569c7)


- **Run Sonar Scanner**  

 > *Execute SonarScanner to analyze the code and send results to SonarQube.*
 ```
 mvn clean verify -DskipTests sonar:sonar \
  -Dsonar.projectKey=salary-api \
  -Dsonar.host.url=http://localhost:9000 \
  -Dsonar.login=sqa_d454c3fc62931070e4d56d27884ef13519fe5d0e # Your token generated in SonarQube
 ```

- **Analyze SonarQube Dashboard**  

 > *Review bugs, vulnerabilities, and other code quality metrics in the dashboard.*

 ![image](https://github.com/user-attachments/assets/e8194959-579a-4caa-8512-f448615f5083)

- **Prioritize and Fix Issues**  

 > *Address critical bugs and refactor code as needed.*

- **Document and Share Findings**  

 > *Summarize the bug analysis results for the team.*


## Conclusion  
Among the various tools discussed, **SonarQube** stands out due to its ability to perform both static and dynamic analysis, offer detailed dashboards, and integrate well with CI/CD pipelines. It is highly recommended for medium to large Java projects for continuous bug tracking and quality monitoring.

## Contact Information  

| Name          | Email Address                              |  
|---------------|--------------------------------------------|  
| Yuvraj Singh  | yuvraj.singh.snaatak@mygurukulam.co         |  

## References  

| Source                                                                                     | Description                                              |
| ------------------------------------------------------------------------------------------ | -------------------------------------------------------- |
| [SonarQube Official Documentation](https://docs.sonarqube.org/latest/)                     | Official guide for configuring and using SonarQube.      |
| [Java SE Development Kit (JDK) Downloads](https://www.oracle.com/java/technologies/javase-jdk11-downloads.html) | Download page for Java Development Kit (JDK 11).         |
| [Apache Maven Project](https://maven.apache.org/)                                          | Official website for Maven build automation tool.        |
| [Gradle Build Tool](https://gradle.org/)                                                   | Official site for the Gradle build automation system.    |
| [GitHub - Cloning a Repository](https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository) | Documentation on how to clone repositories from GitHub.  |
| [AWS EC2 Security Groups - Managing Inbound Rules](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-network-security.html#security-group-rules) | AWS guide for configuring inbound rules in security groups. |
 
