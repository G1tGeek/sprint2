# VCS Notification Setup for Branch

### Author
| Created     |  Version   |   Author     |  Modifed   |      Comment      |    Reviewer      |
|-------------|------------|--------------|------------|-------------------|------------------|
| 12-05-2025  |  V1        | Yuvraj Singh |            | Internal Review   | Siddharth Pawar  |
|             |  V2        | Yuvraj Singh |            | L0 Review         | Naveen Haswani |
|             |  V3        | Yuvraj Singh |            | L1 Review         | Deepak Nishad |
|             |  V4        | Yuvraj Singh |            | L2 Review         | Ashwani Singh |



# Table of Content 
1. [Introduction](#introduction)
2. [Workflow](#workflow)
3. [Pre-requisites](#pre-requisites)
4. [Steps to Set up Branch Notification](#steps-to-set-up-branch-notification)
5. [Conclusion](#conclusion)
6. [Contact](#contact)
7. [References](#references )
   

     
# Introduction 
This document provides a clear guide for setting up notifications for branch events (create, delete, (PR)merge) in GitHub. By following these steps, users can stay informed about branch changes in their repositories. This helps improve team collaboration and keeps everyone updated on project progress.


# Workflow

![Untitled Diagram drawio (10)](https://github.com/user-attachments/assets/5bd94634-dd81-41e6-a01f-d25ab1bce438)


## Pre-requisites
- A GitHub account.
- Access to the repository for which you want to receive notifications.

## Steps to Set up Branch Notification

### 1. **Sign in to GitHub**: Go to [GitHub](https://github.com) and log in to your account.




### 2. Create a repository for which you want to configure notifications for Branch(Create,Delete& Merge(PR)).




### 3. Now, click on the repository you created and navigate to the Settings tab at the top.




### 4. Generate an App Password for Gmail: If you are using Gmail, you'll need to generate an App Password for your Google account:

**Go to your Google Account.**

**Navigate to Security -> Signing in to Google -> App Passwords.**

**Choose Mail and select your device, then generate a password and copy it.**


### 5. Add Gmail Credentials to GitHub Secrets:

**Go to your GitHub repository.** **Click on Settings -> Secrets -> Actions -> New repository secret,**Add two secrets:**

**EMAIL_USERNAME: Your Gmail address (e.g., your-email@gmail.com).**

**EMAIL_PASSWORD: The App Password you generated earlier from Gmail.**



### 6. Set up GitHub Action Workflow:

**Create a GitHub Actions workflow file in your repository to send an email when a Branch- create, Merge(PR) & Delete.**

**In your GitHub repository, create a workflow file in .github/workflows/ (e.g., send-email-on-Branch-notification.yml):**



### 7. Commit and Push the Workflow File:

**Once you add the workflow file, every time a commit is pushed to the specified repo (e.g., Branch-Notification-demo), the GitHub Action will send an email with the details of the commit (message, author, and URL).**



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
