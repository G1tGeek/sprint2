# Bugs Analysis : Proof of Concept

![image](https://github.com/user-attachments/assets/e065c14b-f67c-4cc4-ac3f-15d07034cf99)


## Author
|  Version   |   Author     |  Modifed   |      Comment      |    Reviewer      |
|------------|--------------|------------|-------------------|------------------|
|  V1        | Yuvraj Singh |            | Internal Review   | Siddharth Pawar  |
|  V2        | Yuvraj Singh |            | L0 Review         | Naveen Haswani |
|  V3        | Yuvraj Singh |            | L1 Review         | Deepak Nishad |
|  V4        | Yuvraj Singh |            | L2 Review         | Ashwani Singh |

## Introduction
This document offers a straightforward guide to identifying and addressing bugs in Java code. Implementing systematic bug analysis ensures that developers detect issues early, improve code reliability, and maintain application performance and security.

## What and Why Bug Analysis?

To get a detailed about bug analysis in java [click here]().

## Prerequisites

| Dependency   | Minimum Version |
| ------------ | --------------- |
| Operating System | Ubuntu 22.04 |
| CPU    | 2 vCPU  |
| **Hard Disk   | 25 GB  |
| RAM           | 4 GB     |
| Java JDK     | 17+             |
| PostgreSQL   | Latest Stable   |
| unzip        | Latest Stable   |
| SonarQube    | Latest Stable   |
| SonarScanner | Latest Stable   |
| Maven        | 3.6+            |
| SonarQube | 9000 (open)        |
| Secure HTTPS web traffic | 443  |       
| PostgreSQL database access | 5432  | 


## Steps of Conduct

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
  cd /opt
  sudo wget "https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-25.5.0.107428.zip" -O sonarqube.zip
  sudo unzip sonarqube.zip
  sudo mv sonarqube-25.5.0.107428 sonarqube
  sudo chown -R $USER:$USER sonarqube
  echo "export PATH=$PATH:/opt/sonarqube/bin/linux-x86-64" >> ~/.bashrc
  source ~/.bashrc
  ```

  ![image](https://github.com/user-attachments/assets/7e440c76-f4b5-4a1b-9240-394116cf7ed1)

- **Install SonarScanner**

  ```
  cd /opt
  sudo wget "https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-7.1.0.4889-linux-x64.zip" -O sonar-scanner.zip
  sudo unzip sonar-scanner.zip
  sudo mv sonar-scanner-7.1.0.4889-linux-x64 sonar-scanner
  sudo chown -R $USER:$USER sonar-scanner
  echo "export PATH=$PATH:/opt/sonar-scanner/bin" >> ~/.bashrc
  source ~/.bashrc
  ```

  ![image](https://github.com/user-attachments/assets/e863f3f2-770d-41d6-908f-8374f905f610)

- **Install Maven**

  *Install Maven* [Go to this link](https://github.com/snaatak-Downtime-Crew/Documentation/blob/main/common_stack/application/java/maven/sop/README.md#step-2-install-maven-and-check-version) and follow `Step 2: Install Maven and check version`.

  ![image](https://github.com/user-attachments/assets/149474b7-83b8-4ddb-8947-acf3497309f8)

### Configuration

- **PostgreSQL**-

  > *Access psql terminal*

  ```
  sudo -u postgres psql
  ```

  ![image](https://github.com/user-attachments/assets/7f1a4fab-a503-4bc0-b3ee-b28fa46d3a60)

  > *Create user and database forSonarQube*

  ```
  CREATE USER sonar WITH PASSWORD 'sonar123';
  CREATE DATABASE sonarqube OWNER sonar;
  ```
  
  ![image](https://github.com/user-attachments/assets/acc14c05-71e1-49fd-8d86-0b00eb909b21)

  > *Quit*
  
  ```
  \q
  ```

  ![image](https://github.com/user-attachments/assets/28c9b0c1-f5b3-4e98-8f6b-f41857ba6aef)


- **SonarQube**

  > *Edit the configuration file at `/opt/sonarqube/conf/sonar.properties and update the database settings`*
  
  ```
  sonar.jdbc.username=sonar # line 25
  sonar.jdbc.password=sonar123 # line 26
  sonar.jdbc.url=jdbc:postgresql://localhost/sonarqube # line 43
  sonar.web.host=0.0.0.0 # line 100
  ```

  ![image](https://github.com/user-attachments/assets/ad0050e0-6a00-4af4-8be9-4b13510fe6fd)

- **SonarScanner**

  > *Edit the configuration file at `/opt/sonar-scanner/conf/sonar-scanner.properties` and add your SonarQube server URL*

  ```
  sonar.host.url=http://localhost:9000
  ```

  ![image](https://github.com/user-attachments/assets/37dc2953-8948-4b2e-9361-d57f892e43d6)

### Conducting the Tests  

*Clone your [Salary API](https://github.com/OT-MICROSERVICES/salary-api.git) project repository from GitHub*

![image](https://github.com/user-attachments/assets/21c5c5ae-14d0-4d86-b769-8f5e47a305a8)

- **Start SonarQube Server**  

  > *Launch the SonarQube server and ensure port 9000 is accessible.*

  ```
  sonar.sh start
  ```

  
- **Generate SonarQube Authentication Token**  

*Log into SonarQube, and create an authentication token for scanning.*

### Configure the Project for SonarQube  

*Add SonarQube plugin configuration to your Maven or Gradle build files.*

### Run Sonar Scanner  

*Execute SonarScanner to analyze the code and send results to SonarQube.*

### Analyze SonarQube Dashboard  

*Review bugs, vulnerabilities, and other code quality metrics in the dashboard.*

### Prioritize and Fix Issues  

*Address critical bugs and refactor code as needed.*

### Document and Share Findings  

*Summarize the bug analysis results for the team.*


## Conclusion  
Among the various tools discussed, **SonarQube** stands out due to its ability to perform both static and dynamic analysis, offer detailed dashboards, and integrate well with CI/CD pipelines. It is highly recommended for medium to large Java projects for continuous bug tracking and quality monitoring.

## Contact Information  

| Name          | Email Address                              |  
|---------------|--------------------------------------------|  
| Yuvraj Singh  | yuvraj.singh.snaatak@mygurukulam.co         |  

## References  

- [SonarQube Official Documentation](https://docs.sonarqube.org/latest/)  
- [Java SE Development Kit (JDK) Downloads](https://www.oracle.com/java/technologies/javase-jdk11-downloads.html)  
- [Apache Maven Project](https://maven.apache.org/)  
- [Gradle Build Tool](https://gradle.org/)  
- [GitHub - Cloning a Repository](https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository)  
- [AWS EC2 Security Groups - Managing Inbound Rules](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-network-security.html#security-group-rules)  
