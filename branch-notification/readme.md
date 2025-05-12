# VCS Notification Setup for Branch

### Author
| Created     |  Version   |   Author     |  Modifed   |      Comment      |    Reviewer      |
|-------------|------------|--------------|------------|-------------------|------------------|
| 12-05-2025  |  V1        | Yuvraj Singh |            | Internal Review   | Siddharth Pawar  |
|             |  V2        | Yuvraj Singh |            | L0 Review         | Naveen Haswani |
|             |  V3        | Yuvraj Singh |            | L1 Review         | Deepak Nishad |
|             |  V4        | Yuvraj Singh |            | L2 Review         | Ashwani Singh |



## Table of Contents

<details>
<summary>1. Introduction</summary>

- [Introduction](#introduction)

</details>

<details>
<summary>2. Workflow</summary>

- [Pre-requisites](#pre-requisites)  
- [Steps to Set up Branch Notification](#steps-to-set-up-branch-notification)  
  - [1. Sign in to GitHub](#1-sign-in-to-github)  
  - [2. Setup Repository](#2-setup-repository)  
  - [3. Setup App Password](#3-setup-app-password)  
  - [4. Add Gmail Credentials to GitHub Secrets](#4-add-gmail-credentials-to-github-secrets)  
  - [5. Set up GitHub Action Workflow](#5-set-up-github-action-workflow)  
  - [6. Commit and Push the Workflow File](#6-commit-and-push-the-workflow-file)

</details>

<details>
<summary>3. Wrap-up</summary>

- [Conclusion](#conclusion)  
- [Contact](#contact)  
- [References](#references)

</details>
   

     
# Introduction 
This document offers a straightforward guide to configuring notifications for branch events—such as creation, deletion, and pull request merges—on GitHub. Implementing these steps ensures that users remain informed about changes to branches, enhancing team collaboration and keeping all stakeholders aligned with the project's progress.


# Workflow

![image](https://github.com/user-attachments/assets/8b1b3e25-e6df-4501-abc4-95ae7970dffe)

## Pre-requisites
- A GitHub account.
- Access to the GitHub repository for which you want to receive notifications.

## Steps to Set up Branch Notification

### 1. *Sign in to GitHub*
> *Go to [GitHub](https://github.com) and log in to your account.*

![image](https://github.com/user-attachments/assets/72f0026c-c7d7-4e2e-8f10-c8b4372d4039)

### 2. *Setup Repository*
> *Go-to Your Organization and Create a repository for which you want to configure notifications for Branch(Create,Delete& Merge(PR)).*

![image](https://github.com/user-attachments/assets/f972b2d7-3d65-47b4-a627-c267c9c9b877)

![image](https://github.com/user-attachments/assets/38e7f99b-6b84-4b82-8667-457fb0accaaa)

*Check how to create an organization [here.]()*

### 3. *Setup App Password*
> *Generate an App Password for Gmail: If you are using Gmail, you'll need to generate an App Password for your Google account:*

*Go to your Google Account.*

`Navigate to Security -> Signing in to Google -> App Passwords.`

`Choose Mail and select your device, then generate a password and copy it.`

![image](https://github.com/user-attachments/assets/7f6cccb1-b4d0-4b79-a6c0-1c62bf58580d)


### 4. *Add Gmail Credentials to GitHub Secrets*

> *Go to your GitHub repository.* `Click on Settings -> Secrets` -> `Actions -> New repository secret,Add two secrets:`

`USERNAME: Your Gmail address (e.g., your-email@gmail.com).`

`PASSWD: The App Password you generated earlier from Gmail.`

![image](https://github.com/user-attachments/assets/c08a6202-1e50-4a95-8c1b-8c8deb596895)

### 5. *Set up GitHub Action Workflow*

*Go-to `GitHub Actions` -> `Configure` under **`Simple workflow`** in your repository to send an email when a Branch- create, Merge(PR) & Delete.*

![image](https://github.com/user-attachments/assets/9ad064fa-269f-4a6c-aad7-50fb25694f2d)

*Create a workflow file in .github/workflows/ (e.g., email-on-branch-action.yml) with content:*
```
name: Branch Event Email Notification

on:
  create:
    branches:
      - '**'
  delete:
    branches:
      - '**'
  pull_request:
    types:
      - closed

jobs:
  notify:
    runs-on: ubuntu-latest
    if: |
      github.event_name == 'create' ||
      github.event_name == 'delete' ||
      (github.event_name == 'pull_request' && github.event.pull_request.merged == true)
    steps:
      - name: Send Branch Event Email
        uses: dawidd6/action-send-mail@v3
        with:
          server_address: smtp.gmail.com
          server_port: 465
          username: ${{ secrets.USERNAME }}
          password: ${{ secrets.PASSWD }}
          subject: >
              Branch Event: 
            ${{ github.event_name == 'create' && 'Created' || github.event_name == 'delete' && 'Deleted' || 'Merged PR' }}
            in ${{ github.repository }}
          to: 71yuvrajsingh6123@gmail.com
          from: GitHub Actions <${{ secrets.EMAIL_USERNAME }}>
          html_body: |
            <h2>Branch Event Notification</h2>
            <p><strong>Repository:</strong> ${{ github.repository }}</p>
            <p><strong>Event Type:</strong> 
              ${{ github.event_name == 'create' && 'Branch Created' || github.event_name == 'delete' && 'Branch Deleted' || 'Pull Request Merged' }}
            </p>
            <p><strong>Branch:</strong> 
              ${{ github.event.ref || github.event.pull_request.base.ref }}
            </p>
            <p><strong>Initiator:</strong> 
              ${{ github.actor }}
            </p>
            <p>
              ${{
                github.event_name == 'pull_request' 
                && format('<a href="https://github.com/{0}/pull/{1}">View PR</a>', github.repository, github.event.pull_request.number)
                || ''
              }}
            </p>

```
![image](https://github.com/user-attachments/assets/1bcc00e9-d478-464a-a9f6-599e6803bb58)


### 6. *Commit and Push the Workflow File*

*Once you add the workflow file, every time a Branch Action is performed to the specified repo , the GitHub Action will send an email with the details of the commit.*

![image](https://github.com/user-attachments/assets/29a968bf-697d-4c2b-b723-020cc5747996)


## Conclusion
The POC successfully implements an email notification system that triggers on critical branch events: creation, deletion, and merging(PR) of branches in a GitHub repository. It leverages GitHub Actions to automatically send notifications, ensuring that team members are promptly informed of important branch activities, enhancing collaboration and workflow monitoring.

## Contact

| Name| Email Address      |
|-----|--------------------------|
| Yuvraj Singh | yuvraj.singh.snaatak@mygurukulam.co |
 
## References 
|links | Description |
|-------|------------|
|https://youtu.be/oMU9MUIXPyI?feature=shared|**Rainbow talks** |
|https://www.youtube.com/watch?v=qToZN5S67AM| **SDet Automation**|
|https://tinyurl.com/bdpf3ajc|**GIT**|
