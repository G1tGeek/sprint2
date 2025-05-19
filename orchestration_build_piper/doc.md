# BuildPiper Documentation

![Logo](https://i.ytimg.com/vi/g9UZDLvZlqc/maxresdefault.jpg)

### Author
| Version | Author        | Modified     | Comment           | Reviewer         |
|---------|---------------|--------------|-------------------|------------------|
| V1.0    | Yuvraj Singh  | 19-05-2025   | Initial Draft     | Siddharth Pawar  |

---

## Table of Contents

<details>
<summary>1. Introduction</summary>

- [Introduction](#introduction)  
- [What is BuildPiper?](#what-is-buildpiper)  
- [Why Use BuildPiper?](#why-use-buildpiper)

</details>

<details>
<summary>2. Core Concepts</summary>

- [Workflow Diagram](#workflow-diagram)  
- [Key Features](#key-features)  
- [Advantages](#advantages)

</details>

<details>
<summary>3. Best Practices</summary>

- [Best Practices](#best-practices)

</details>

<details>
<summary>4. Wrap-up</summary>

- [Conclusion](#conclusion)  
- [Contact](#contact)  
- [References](#references)

</details>

---

## Introduction

This guide provides a comprehensive overview of BuildPiper—a robust microservices delivery platform designed to simplify and accelerate application development and deployment. It covers BuildPiper’s key features, core concepts, workflow architecture, operational advantages, and best practices. By understanding and using BuildPiper effectively, DevOps engineers and development teams can build, deploy, and manage scalable, secure, and high-performance microservices applications with greater efficiency and control.

---

## What is BuildPiper?

BuildPiper is an end-to-end **Microservices Delivery Platform (MDP)** that enables rapid onboarding, configuration, and continuous delivery of microservices with minimal manual intervention. It offers a unified interface to manage CI/CD pipelines, security scans, Kubernetes environments, and governance policies.

BuildPiper integrates seamlessly with modern DevOps toolchains and empowers teams to deploy, manage, and monitor services across multiple environments using standardized workflows and best practices.

---

## Why Use BuildPiper?

| **Benefit**              | **Description**                                                                 |
|--------------------------|---------------------------------------------------------------------------------|
| **Unified Platform**     | Centralizes CI/CD, security, monitoring, and Kubernetes ops in one dashboard.   |
| **Faster Time-to-Market**| Automates repetitive tasks and reduces manual DevOps overhead.                 |
| **Enterprise Governance**| Enforces compliance, role-based access, and approval workflows.                |
| **Secure by Design**     | Integrated vulnerability scans and policy enforcement at every stage.         |
| **Cloud-Native Ready**   | Optimized for microservices and Kubernetes-based architectures.                |

---

## Architecture

![image](https://github.com/user-attachments/assets/9d759234-fd75-4978-9c0a-24a0255612e2)

---

### 1. **BP Gateway**
- Acts as the **entry point** for all external and internal requests.
- Manages API routing, authentication, and access control.
- Ensures secure and scalable communication between clients and the internal system.

---

### 2. **BPCTL & Frontend**
- **BPCTL** is a Git-based CLI tool used for interacting with BuildPiper through configuration files.
- **Frontend** provides a web-based UI for visualizing pipelines, jobs, configurations, and metrics.
- These tools allow both **developers and platform engineers** to interact with the system effectively.

---

### 3. **Platform API**
- The core service that acts as a bridge between the frontend/CLI and the backend systems.
- Orchestrates workflows, handles REST requests, and performs validations.
- All job execution, resource provisioning, and platform operations are funneled through this layer.

---

### 4. **Core Backend Services**

| Component     | Description |
|---------------|-------------|
| **Redis**     | Used for **caching** and **message brokering**, improving performance and event-driven workflows. |
| **Database**  | Stores system state, job metadata, user configs, secrets, and audit logs. |
| **Deploy API**| Handles the deployment lifecycle of applications (build, release, deploy, rollback). |
| **Scheduler** | Orchestrates job execution order, retries, and time-based scheduling across templates. |

---

### 5. **Job Templates and Job Steps**
- **Job Templates** define reusable CI/CD workflows for common DevOps tasks.
- Each **Job Template** contains multiple **Job Steps**, executed sequentially:
  - Example steps: `Build`, `Test`, `Push`, `Deploy`, `Health Check`.
- This modular design allows consistent and versioned automation across projects.

---

### 6. **Shared File System**
- Enables **persistent and shared storage** for files across jobs and agents.
- Useful for transferring artifacts, logs, and temporary build files between steps and services.

---

### 7. **BP Agent**
- Installed on target environments (e.g., clusters, VMs).
- Executes actual deployment tasks, runs jobs, and reports back status.
- Enables hybrid/multi-cloud support and remote environment provisioning.

---

## Key Features

| **Feature**                     | **Description**                                                                 |
|---------------------------------|---------------------------------------------------------------------------------|
| **Microservices Onboarding**    | Quickly onboard services with Git, container, and runtime configuration.       |
| **Custom CI/CD Pipelines**      | Build and deploy using drag-and-drop or declarative YAML workflows.           |
| **Security Integration**        | Run static and dynamic code analysis, vulnerability scans in CI pipeline.      |
| **Environment Management**      | Manage multiple Kubernetes clusters, namespaces, and secrets.                 |
| **Role-Based Access Control**   | Define granular roles and permissions per team, service, or environment.       |
| **Audit Logging**               | Maintain traceability across all user actions and deployments.                |
| **Observability Integration**   | Built-in monitoring and logging with plug-ins for Prometheus, Grafana, ELK.   |
| **Helm & K8s Native**           | Supports Helm charts, Kubernetes manifests, and GitOps workflows.             |

---

## Advantages

| **Advantage**                   | **Impact**                                                                     |
|----------------------------------|---------------------------------------------------------------------------------|
| **Low-Code DevOps**              | Reduced need for complex scripts or custom integrations.                       |
| **Operational Efficiency**       | Automates common tasks like scanning, approvals, deployment, and rollback.     |
| **Developer Empowerment**        | Developers can own deployment pipelines without heavy DevOps dependencies.     |
| **Reduced Downtime**             | Built-in rollback and deployment health checks improve stability.              |
| **Consistent Standards**         | Enforces repeatable patterns and governance across all services.               |

---

## Best Practices

| **Practice**                          | **Description**                                                                |
|--------------------------------------|--------------------------------------------------------------------------------|
| **Modularize Pipelines**             | Break down pipelines into reusable steps and templates.                        |
| **Scan Early, Scan Often**           | Integrate SAST/DAST tools early in the CI pipeline.                            |
| **Role-based Access**                | Assign roles based on least privilege to ensure secure team collaboration.     |
| **Use GitOps for Deployments**       | Enable traceability and version control by deploying through GitOps patterns.  |
| **Monitor All Environments**         | Ensure real-time observability across dev, staging, and production.            |
| **Define Promotion Workflows**       | Establish approval gates between environments for controlled deployments.      |

---

## Conclusion

BuildPiper enables DevOps and engineering teams to efficiently build, secure, deploy, and monitor microservices at scale. With its comprehensive feature set, governance controls, and automation capabilities, BuildPiper reduces the operational burden while ensuring application delivery remains fast, compliant, and resilient. By adopting BuildPiper, teams can establish consistent DevSecOps practices and accelerate innovation in modern, cloud-native environments.

---

## Contact

| Name          | Email Address                              |
|---------------|--------------------------------------------|
| Yuvraj Singh  | yuvraj.singh.snaatak@mygurukulam.co         |

---

## References

| **Resource**                      | **Link**                                               |
|----------------------------------|--------------------------------------------------------|
| BuildPiper Official Website      | [Visit](https://buildpiper.io/)                        |
| BuildPiper Blog                  | [Visit](https://buildpiper.io/blog/)                   |
| CI/CD Best Practices             | [Visit](https://www.redhat.com/en/topics/devops/what-is-ci-cd) |
