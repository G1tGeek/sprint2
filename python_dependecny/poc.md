
# Dependency Vulnerability Scanning: Proof of Concept

![image](https://github.com/user-attachments/assets/7b825f31-17a1-49c1-b924-f7c525d0e8b9)

## Author

| Version | Author       | Modified | Comment       | Reviewer         |
|---------|--------------|----------|---------------|------------------|
| V1      | Yuvraj Singh |          | Internal Review | Siddharth Pawar  |
| V2      | Yuvraj Singh |          | L0 Review     | Naveen Haswani   |
| V3      | Yuvraj Singh |          | L1 Review     | Deepak Nishad    |
| V4      | Yuvraj Singh |          | L2 Review     | Ashwani Singh    |

## Table of Contents

<details>
<summary>1. Introduction</summary>

- [Introduction](#introduction)  
- [What and Why Dependency Scanning?](#what-and-why-dependency-scanning)  

</details>

<details>
<summary>2. Steps of Conduct</summary>

- [Prerequisites](#prerequisites)
- [Install Dependencies](#install-dependencies)
- [Running pip-audit](#running-pip-audit)
- [Analyzing Results](#analyzing-results)

</details>

<details>
<summary>3. Wrap-up</summary>

- [Conclusion](#conclusion)  
- [Contact Information](#contact-information)  
- [References](#references)  

</details>

## Introduction

This document provides a step-by-step guide to perform dependency vulnerability scanning on Python projects using `pip-audit`. By identifying known vulnerabilities in project dependencies, developers can proactively address security issues and maintain the integrity of their applications.

## What and Why Dependency Scanning?

[Click here]() for a detailed and informative guide on dependency scanning with python.

## Steps of Conduct

### Prerequisites

| Dependency       | Minimum Version |
|------------------|-----------------|
| Operating System | Ubuntu 22.04    |
| Python           | 3.8+            |
| pip              | 20.0+           |
| pip-audit        | Latest          |
| Git              | Latest          |

### Install Dependencies

1. **Update and Upgrade Packages**

    *[Go to this link](https://github.com/snaatak-Downtime-Crew/Documentation/blob/main/common_stack/operating_system/ubuntu/sop/commoncommands/README.md#1-basic-system-commands) and follow `STEP 3. Update and Upgrade Packages`.*

2. **Install apt packages**

    *[Go to this link](https://github.com/snaatak-Downtime-Crew/Documentation/tree/main/common_stack/operating_system/ubuntu/sop/softwaremanagement#3-Install-a-Software) and follow `3. Install a Software` Package name: python3, python3-pip, python3.12-venv*
  
3. **Install pip-audit**

   *Use pip to install a pip package*

   ```
   sudo pip install pip-audit --break-system-packages
   ```

   ![image](https://github.com/user-attachments/assets/e9594ef4-c42e-4d12-a47a-d236838d7f9d)

### Running pip-audit

1. **Clone the Repositories**

    *Clone the [Notification API](https://github.com/OT-MICROSERVICES/notification-worker.git) and [Attendance API](https://github.com/OT-MICROSERVICES/attendance-api.git) from github.*

    ![image](https://github.com/user-attachments/assets/0180da62-db96-4882-8232-22882a0eb0b6)



2. **Audit Dependencies**
  
  > **Attendance API**

  - *Create a virtual environment venv1 for Attendacne API and activate it*
    
    ```
    python3 -m venv venv1
    source venv1/bin/activate
    ```

    ![image](https://github.com/user-attachments/assets/0cd9b861-d70a-4410-a064-ccec06022486)

  - *Check if requirement.txt exists. If not create a requirements.txt with:*
    ```
    pip freeze requirements.txt
    ```
    
    ![image](https://github.com/user-attachments/assets/568b446b-c871-4745-b740-a83c7442a64e)

  - *Audit the file.*
    
    ```
    pip-audit -r requirements.txt
    ```
    
    ![image](https://github.com/user-attachments/assets/c1dfd112-b906-4c76-8858-00342a1aae3d)

  - *Deactivate the virtual environment*

    ```
    deactivate
    ```

    ![image](https://github.com/user-attachments/assets/a36d195f-8559-41ad-804e-f34d74ede392)

  > **Notification Worker**

  - *Create a virtual environment venvn2 for notification worker and activate it*
    
    ```
    python3 -m venv venv2
    source venv2/bin/activate
    ```

    ![image](https://github.com/user-attachments/assets/7c1dd836-7a12-4af1-9fbf-f040c7700f7f)

  - *Check if requirement.txt exists. If not create a requirements.txt with:*
    ```
    pip freeze requirements.txt
    ```

    ![image](https://github.com/user-attachments/assets/17badc14-3b7c-4b76-842f-2a8be28854fc)
    > *Already exists here*
    
  - *Audit the file.*
    
    ```
    pip-audit -r requirements.txt
    ```
    
    ![image](https://github.com/user-attachments/assets/9e8418e3-16ea-4ee1-a809-dbbd310d613b)

  - *Deactivate the virtual environment*

    ```
    deactivate
    ```

    ![image](https://github.com/user-attachments/assets/4e58e471-a99a-4766-8f91-7ef43058a827)

### Analyzing Results

- **Review Vulnerabilities**

  Examine the output to identify packages with known vulnerabilities.

- **Update Insecure Packages**

  Modify `requirements.txt` to specify secure versions and update:

  ```bash
  pip install --upgrade -r requirements.txt
  ```

- **Re-run pip-audit**

  Ensure all vulnerabilities have been addressed:

  ```bash
  pip-audit -r requirements.txt
  ```

## Conclusion

Implementing `pip-audit` for dependency scanning in Python projects like `attendance-api` and `notification-worker` enhances security by identifying and mitigating known vulnerabilities in third-party packages. Regular audits and prompt updates are essential for maintaining robust and secure applications.

## Contact Information

| Name         | Email Address                             |
|--------------|-------------------------------------------|
| Yuvraj Singh | yuvraj.singh.snaatak@mygurukulam.co       |

## References

| Source                                                                                     | Description                                              |
|--------------------------------------------------------------------------------------------|----------------------------------------------------------|
| [pip-audit Documentation](https://pypi.org/project/pip-audit/)                             | Official guide for using pip-audit.                      |
| [Python Packaging Advisory Database](https://github.com/pypa/advisory-database)            | Database of known Python package vulnerabilities.        |
| [GitHub - attendance-api](https://github.com/OT-MICROSERVICES/attendance-api.git)          | Repository for attendance-api project.                   |
| [GitHub - notification-worker](https://github.com/OT-MICROSERVICES/notification-worker.git)| Repository for notification-worker project.              |
