# Commit Sign-Off: Documentation

![image](https://github.com/user-attachments/assets/32139801-0da3-4f2b-b905-4c783512ecda)

### Author
|  Version   |   Author     |  Modifed   |      Comment      |    Reviewer      |
|------------|--------------|------------|-------------------|------------------|
|  V1        | Yuvraj Singh |            | Internal Review   | Siddharth Pawar  |
|  V2        | Yuvraj Singh |            | L0 Review         | Naveen Haswani |
|  V3        | Yuvraj Singh |            | L1 Review         | Deepak Nishad |
|  V4        | Yuvraj Singh |            | L2 Review         | Ashwani Singh |

---

## Table of Contents

<details>
<summary>1. Introduction</summary>

- [Introduction](#introduction)  
- [What is Commit Sign-Off?](#what-is-commit-sign-off)  
- [Why Commit Sign-Off in CI?](#why-commit-sign-off-in-ci)

</details>

<details>
<summary>2. Workflow & Benefits</summary>

- [Workflow](#workflow)  
- [Advantages of Commit Sign-Off in CI](#advantages-of-commit-sign-off-in-ci)

</details>

<details>
<summary>3. Walkthrough</summary>

- [Proof of Concept](#proof-of-concept)
- [Best Practices](#best-practices) 

</details>

<details>
<summary>4. Best Practices & Wrap-up</summary>
  
- [Conclusion](#conclusion)  
- [Contact](#contact)  
- [References](#references)

</details>


---

## Introduction

This document offers a straightforward guide to integrating commit sign-off as a generic CI operation inside an application CI design. Implementing this step ensures that contributors are verified and accountable, enhancing code traceability and aligning with organizational compliance and collaboration standards.

---

## What is Commit Sign-Off?

Commit sign-off is a declaration by a contributor that they have the right to submit the code under the project’s license. It is included in the commit message using a line such as:

Signed-off-by: Developer Name <email@example.com>

It supports the Developer Certificate of Origin (DCO) and helps maintain accountability in both open-source and enterprise CI systems.

---

## Why Commit Sign-Off in CI?

Including commit sign-off as a generic CI operation offers several benefits:

- Ensures compliance with contribution and licensing policies
- Prevents unauthorized code submissions
- Creates an audit trail of contributions
- Enforces contributor responsibility
- Integrates well with CI pipelines for automation

---

## Workflow 

![image](https://github.com/user-attachments/assets/72fdebf9-c9cc-447f-9afb-2c53da1f3882)

1. **Developer Commit**: The developer commits code with a mandatory `Signed-off-by` line.
2. **Pre-Check/Hook**: A Git hook or CI job verifies that each commit contains a valid sign-off.
3. **CI Pipeline Triggered**: If the sign-off passes, the CI pipeline is triggered automatically.
4. **Build and Test**: The application is built and tested in stages.
5. **Report and Notify**: The pipeline reports results and sends notifications. If sign-off is missing, the process halts early.

---

## Advantages of Commit Sign-Off in CI

| Advantage                     | Description                                                                 |
|-------------------------------|-----------------------------------------------------------------------------|
| Traceability                  | Identifies the responsible developer for each commit.                      |
| Legal Clarity                 | Confirms contributor agreement to licensing terms.                         |
| Automation Friendly           | Easily validated by CI tools and Git hooks.                                |
| Policy Enforcement            | Enforces contribution rules at the source.                                 |
| Security & Compliance Support| Reduces risks of unauthorized contributions entering production.           |

---

## Proof of Concept

*Refer [this]() document to get a step-by-step guide to perform a Commit Sign-Off.*

---


## Best Practices

- Educate contributors on how and why to use sign-off
- Use automated CI checks or Git hooks to enforce sign-off
- Keep commit message format consistent
- Combine sign-off with mandatory code reviews
- Clearly document sign-off requirements in contribution guides

---

## Conclusion

Commit sign-off adds a critical compliance layer to the CI process. By verifying code ownership and policy agreement at the source, it strengthens the integrity and security of modern development workflows. When combined with automated CI checks, sign-off enforcement supports a scalable and reliable application CI design.

---

## Contact

| Name          | Email Address                              |
|---------------|--------------------------------------------|
| Yuvraj Singh  | yuvraj.singh.snaatak@mygurukulam.co         |

---

## References

| Resource                         | Link                                                |
|----------------------------------|-----------------------------------------------------|
| **Developer Certificate of Origin (DCO)** | [Visit](https://developercertificate.org/) |
| **Git Commit Sign-Off Documentation** | [Visit](https://git-scm.com/docs/git-commit#Documentation/git-commit.txt---signoff) |
| **Jenkins Pipeline Documentation** | [Visit](https://www.jenkins.io/doc/book/pipeline/) |
| **GitHub DCO Action**           | [Visit](https://github.com/probot/dco) |
