# SonarQube | Quality Gates

![Logo](https://www.sonarsource.com/images/logos/sonarqube-logo.png)

### Author
| Created     | Version | Author        | Modified    | Comment           | Reviewer         |
|-------------|---------|---------------|-------------|--------------------|------------------|
| 19-05-2025  | V1.0    | Yuvraj Singh  | --          | Initial Draft      | Siddharth Pawar  |

---

## Table of Contents

<details>
<summary>1. Introduction</summary>

- [Introduction](#introduction)  
- [What is a Quality Gate?](#what-is-a-quality-gate)  
- [Why Use Quality Gates?](#why-use-quality-gates)

</details>

<details>
<summary>2. Quality Gates in Depth</summary>

- [Workflow](#workflow-diagram)  
- [Advantages](#advantages)  
- [Best Practices](#best-practices)

</details>

<details>
<summary>3. Wrap-up</summary>

- [Conclusion](#conclusion)  
- [Contact](#contact)  
- [References](#references)

</details>

---

## Introduction

This document explains the concept of **Quality Gates** in **SonarQube**, a vital feature for enforcing code quality and compliance across your CI/CD pipelines. It provides insight into what quality gates are, why they matter, and how they improve your development lifecycle.

---

## What is a Quality Gate?

A **Quality Gate** in SonarQube is a set of predefined conditions that code must meet to be considered acceptable. These gates assess the results of a code scan and determine whether the code passes or fails the quality check.

### Default Conditions Often Include:

| Metric                       | Condition                      |
|-----------------------------|--------------------------------|
| New Bugs                    | 0                              |
| New Vulnerabilities         | 0                              |
| New Code Coverage           | ≥ 80%                          |
| New Code Duplications       | ≤ 3%                           |
| Maintainability Rating      | A                             |
| Security Rating             | A                             |
| Reliability Rating          | A                             |

If any condition is not met, the Quality Gate status becomes **Failed**.

---

## Why Use Quality Gates?

| Benefit                        | Description                                                                 |
|-------------------------------|-----------------------------------------------------------------------------|
| **Enforces Standards**        | Ensures every commit or merge meets coding standards and security baselines. |
| **CI/CD Integration**         | Automatically fails pipelines when code quality is poor.                    |
| **Prevent Technical Debt**    | Stops poorly written code from progressing to production.                   |
| **Increased Developer Awareness** | Developers receive immediate feedback about code quality.            |
| **Better Maintainability**    | Cleaner code leads to easier maintenance and fewer bugs in the long run.    |

---

## Workflow Diagram

```mermaid
flowchart TD
    A[Code is Committed] --> B[SonarQube Analyzes Code]
    B --> C[Quality Gate is Applied]
    C -->|Pass| D[Pipeline Continues]
    C -->|Fail| E[Pipeline is Blocked]
    E --> F[Developer Fixes Issues]
    F --> B
```

---

| **Advantage**                   | **Description**                                                                                |
| ------------------------------- | ---------------------------------------------------------------------------------------------- |
| **Automated Quality Control**   | Enforces predefined code quality standards automatically during analysis.                      |
| **Immediate Feedback**          | Provides real-time feedback to developers after every code commit or scan.                     |
| **CI/CD Integration**           | Seamlessly integrates with Jenkins, GitLab CI, and other pipelines to enforce quality gates.   |
| **Reduces Technical Debt**      | Prevents bad code from being merged, thus reducing long-term maintenance overhead.             |
| **Customizable Criteria**       | Teams can define and tune quality gates based on severity levels, coverage, duplications, etc. |
| **Improves Code Reliability**   | Promotes best coding practices, resulting in more secure and stable code.                      |
| **Supports Multiple Languages** | Quality gates work across many languages, including Java, Python, JavaScript, and more.        |

---

| **Best Practice**                   | **Description**                                                                                 |
| ----------------------------------- | ----------------------------------------------------------------------------------------------- |
| **Define Clear Thresholds**         | Set strict but realistic thresholds for bugs, vulnerabilities, code coverage, and duplications. |
| **Use 'Fail' as Default Behavior**  | Configure quality gates to fail builds when critical metrics are violated.                      |
| **Treat Warnings Seriously**        | Address warnings proactively to avoid future escalations to bugs or vulnerabilities.            |
| **Review and Update Regularly**     | Periodically revise quality gate rules to adapt to evolving project requirements.               |
| **Integrate Early in the Pipeline** | Place SonarQube scans early in the CI process to catch issues before review or deployment.      |
| **Educate Your Team**               | Ensure all developers understand quality gate criteria and why they matter.                     |
| **Leverage Quality Profiles**       | Use customized quality profiles aligned with team standards to reinforce meaningful rules.      |

---

## Conclusion

From the Quality Gates analysis of `Salayr API`, I found that the code needs some cleanup—like making it easier to understand, removing repeated parts, and using consistent names and comments. Also, using commit sign-off helps make sure the code is safe and properly checked in the CI process.

---

## References

### References

- [SonarQube Documentation – Quality Gates](https://docs.sonarsource.com/sonarqube/latest/project-administration/quality-gates/)
- [SonarQube Rules and Quality Profiles](https://docs.sonarsource.com/sonarqube/latest/quality-profiles/rules/)
- [SonarQube Supported Languages](https://docs.sonarsource.com/sonarqube/latest/requirements/requirements/)
