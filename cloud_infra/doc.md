# Cloud Infrastructure Design: Dev Environment Documentation

## Author & Version History

| Version | Author        | Modified | Comment         | Reviewer         |
|---------|---------------|----------|------------------|------------------|
| V1      | Yuvraj Singh  |          | Internal Review  | Siddharth Pawar  |
| V2      | Yuvraj Singh  |          | L0 Review        | Naveen Haswani   |
| V3      | Yuvraj Singh  |          | L1 Review        | Deepak Nishad    |
| V4      | Yuvraj Singh  |          | L2 Review        | Ashwani Singh    |

## Table of Contents

<details><summary>1. Introduction</summary>

- [Introduction](#introduction)  
- [Purpose of this Infrastructure](#purpose-of-this-infrastructure)  

</details>

<details><summary>2. Pre-requisites</summary>

- [Tools and Accounts Required](#tools-and-accounts-required)  
- [Knowledge Requirements](#knowledge-requirements)  

</details>

<details><summary>3. Infrastructure Diagram</summary>

- [Infra Diagram](#infrastructure-diagram)  

</details>

<details><summary>4. Infrastructure Description</summary>

- [Virtual Network Setup](#virtual-network-setup) 
- [Subnet Structure](#subnet-structure)  
- [Instance Configuration](#instance-configuration)  
- [Load Balancing and DNS](#load-balancing-and-dns)  

</details>

<details><summary>5. Security Groups and NACL</summary>

- [Security Group Rules](#security-group-rules)  
- [Network ACL Rules](#network-acl-rules)  

</details>

<details><summary>6. Wrap-Up</summary>

- [Conclusion](#conclusion)  
- [Contact Information](#contact-information)
- [References](#references) 

</details>

## Introduction

This document outlines the design, components, and security considerations for a cloud-based infrastructure built for a development environment. The infrastructure is built on AWS using best practices for high availability, modular design, and secure access.

### Purpose of this Infrastructure

- To establish a scalable and segregated development environment.  
- To enable smooth integration and deployment of code using CI/CD pipelines.  
- To maintain secure and structured access control using security groups and network ACLs.  
- To support load-balanced and fault-tolerant application services.  

### Tools and Accounts Required

| Tool/Service | Purpose                          |
|--------------|----------------------------------|
| AWS Account  | Cloud hosting & resource creation |
| Terraform    | Infrastructure as Code (IaC)      |
| GitHub       | Version control for IaC           |
| IAM Access   | Programmatic access to AWS        |

### Knowledge Requirements

- Basic AWS Networking (VPC, Subnets, NACLs, Security Groups)  
- Linux administration  
- Terraform scripting and module use  
- Domain setup and Route53 configuration  

## Infrastructure Diagram

![image](https://github.com/user-attachments/assets/ccae11dd-e595-4b79-9df8-8c7bf565ecc7)


### Virtual Network Setup

- **VPC CIDR:** `10.0.0.0/16`  
- Hosted in **two availability zones** for redundancy and high availability.  
- **Internet Gateway** attached to allow internet access for the public subnet.  

### Subnet Structure

| Subnet Name        | CIDR Block     | Type     | AZ           | Purpose                    |
|--------------------|----------------|----------|--------------|----------------------------|
| Public Subnet      | 10.0.1.0/24    | Public   | ap-south-1a  | Nginx reverse proxy        |
| App Subnet         | 10.0.2.0/24    | Private  | ap-south-1a  | Application services       |
| Middleware Subnet  | 10.0.3.0/24    | Private  | ap-south-1a  | Kafka messaging queue      |
| Database Subnet    | 10.0.4.0/24    | Private  | ap-south-1a  | MongoDB                    |

### Instance Configuration

| Component     | AMI           | Instance Type | Ports Used       |
|---------------|---------------|----------------|------------------|
| Nginx Proxy   | Ubuntu 22.04  | t2.micro       | 80, 8080, 9000   |
| App Server    | Ubuntu 22.04  | t2.micro       | 3000             |
| Kafka Broker  | Ubuntu 22.04  | t2.medium      | 9092             |
| MongoDB       | Ubuntu 22.04  | t2.small       | 27017            |

### Load Balancing and DNS

- **Nginx** acts as a reverse proxy, routing requests to internal services based on port:  
  - `nginx.opstree.com:8080` → App Server  
  - `nginx.opstree.com:9000` → Kafka API  
- **Route53** is used for mapping custom domain names to the public IP of Nginx.

### Security Group Rules

| SG Name   | Port Range       | Source     | Purpose                        |
|-----------|------------------|------------|--------------------------------|
| nginx-sg  | 80, 8080, 9000   | 0.0.0.0/0  | Public access to Nginx         |
| app-sg    | 3000             | nginx-sg   | Access from Nginx              |
| kafka-sg  | 9092             | app-sg     | Access from App Server         |
| mongo-sg  | 27017            | kafka-sg   | Kafka producer access          |

### Network ACL Rules

| NACL Name     | Inbound Rules                    | Outbound Rules                | Subnet                     |
|---------------|----------------------------------|-------------------------------|----------------------------|
| public-nacl   | Allow 80, 8080, 9000 from all     | Allow all to all              | Public Subnet              |
| private-nacl  | Allow required internal ports     | Restrict to internal traffic  | App, Middleware, DB Subnets|

- All NACLs have explicit **DENY** rules for unauthorized ports.  
- **Flow logs** are enabled for all subnets for auditing and troubleshooting.


### Conclusion

The designed cloud infrastructure supports a development environment with clear subnet separation, secure access, and domain-based traffic routing. By using Terraform, the environment remains reproducible, maintainable, and easily extendable. Security is enhanced through fine-grained SG and NACL rules, ensuring safe communication between tiers while allowing public exposure only where needed.

### Contact Information

| Name          | Email Address                            |
|---------------|-------------------------------------------|
| Yuvraj Singh  | yuvraj.singh.snaatak@mygurukulam.co       |

### References

| Description                  | Link  |
|------------------------------|-------|
| AWS VPC Documentation        | Visit |
| Terraform AWS Provider       | Visit |
| Network ACLs vs Security Groups | Visit |
| Route53 Domain Mapping       | Visit |
| Nginx as a Reverse Proxy     | Visit |
