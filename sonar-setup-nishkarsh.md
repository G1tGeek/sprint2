# POC to setup SonarQube

| Created     | Last Updated | Version | Author          | Comment         | Reviewer |
|-------------|--------------|---------|-----------------|-----------------|----------|
| 12-05-2025  |  12-05-2025  | V1      | Nishkarsh Kumar | Internal Review | Pritam   |



## Table of Contents

<details>
<summary>1. Introduction</summary>

- [Introduction](#introduction)  
- [Prerequisites](#prerequisites)  

</details>

<details>
<summary>2. Installation</summary>

- [Install Dependencies](#install-dependencies)  
  - [Install Java](#install-java)  
  - [Install PostgreSQL](#install-postgresql)  
  - [Install unzip](#install-unzip)  
  - [Install SonarQube](#install-sonarqube)  
  - [Install SonarScanner](#install-sonarscanner)  

</details>

<details>
<summary>3. Configuration</summary>

- [Configuration](#configuration)  
  - [Configure PostgreSQL](#postgresql)  
  - [Configure SonarQube](#sonarqube)  
  - [Configure SonarScanner](#sonarscanner)  

</details>

<details>
<summary>4. Service Setup</summary>

- [Service for SonarQube](#service-for-sonarqube)  

</details>

<details>
<summary>5. Verification</summary>

- [Check Working](#check-working)  

</details>

<details>
<summary>6. Support</summary>

- [Contact Information](#contact-information)  
- [References](#references)  

</details>


## Introduction

This README provides a comprehensive walkthrough to set up SonarQube, a popular open-source platform for continuous inspection of code quality, including automatic review with static analysis of code to detect bugs, code smells, and security vulnerabilities. This guide covers the installation of required dependencies, SonarQube and SonarScanner setup, PostgreSQL configuration, and service management to help you deploy a production-ready SonarQube instance efficiently.


### Prerequisites

| Dependency   | Minimum Version |
| ------------ | --------------- |
| Java JDK     | 17+             |
| PostgreSQL   | Latest Stable   |
| unzip        | Latest Stable   |

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

### Check working

 > *Go-to SonarQube server at `<public-ip>:9000`*

  ![image](https://github.com/user-attachments/assets/ab8a3843-75d8-42de-96da-033bc5658014)

## Contact Information

| **Name**    | **Email**                |
|-------------|--------------------------|
| Nishkarsh Kumar     | nishkarsh.kumar.snaatak@mygurukulam.co  |

## References  

| Title                          | Link                                                                 |  
|--------------------------------|----------------------------------------------------------------------|  
| GitHub Docs - Enabling 2FA       | [Visit](https://docs.github.com/en/authentication/securing-your-account-with-two-factor-authentication-2fa) |  
| GitHub Docs - Creating a PAT (Classic)                  | [Visit](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens) |  
