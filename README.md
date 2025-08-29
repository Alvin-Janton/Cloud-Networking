# AWS VPC Networking

---

### Introduction

This repository documents a complete hands-on journey with **Amazon Virtual Private Cloud (VPC)**, covering how to design, secure, operate, and extend cloud networks on AWS.  

The projects are organized into three progressive modules, each focusing on a different stage of network management—from core foundations to advanced monitoring and secure service connectivity.  

Each module contains detailed write-ups, architecture diagrams, and command outputs that demonstrate real-world networking workflows.

---

### Projects Included

This repository contains the following VPC-related modules, each with its own dedicated folder, detailed README, and architecture snapshots:

**[VPC-Fundamentals](./VPC-Fundamentals/)**  
  * Covers the basics of VPCs, subnets, route tables, internet gateways, and security groups.  
  * Demonstrates how to configure private and public subnets with dedicated rules and ACLs.  
  * Introduces AWS CLI for faster VPC setup and automation.  

**[VPC-Operations](./VPC-Operations/)**  
  * Deploys EC2 instances into VPC subnets (public and private).  
  * Tests connectivity between instances using `ssh`, `ping`, and `curl`.  
  * Explores troubleshooting steps and builds cross-VPC communication with peering connections.  

**[Advanced-VPC-Operations](./Advanced-VPC-Operations/)**  
  * Implements VPC Flow Logs and CloudWatch Logs Insights for monitoring and analysis.  
  * Connects VPCs securely to S3 using VPC endpoints with fine-grained bucket and endpoint policies.  
  * Demonstrates IAM integration and multi-VPC architectures for secure traffic flow.  

---

### Technologies & Services Used

**Cloud Services:** AWS (VPC, Subnets, Route Tables, Security Groups, NACLs, EC2, S3, IAM, Flow Logs, CloudWatch, VPC Peering)  
**Tools:** AWS CLI, CloudShell, `ssh`, `ping`, `curl`  
**Concepts:** Networking fundamentals, multi-VPC design, private/public subnet isolation, logging & monitoring, endpoint security  

---

### Learning Objectives

- Understand how to design and configure **VPCs, subnets, and gateways**.  
- Apply **security controls** with security groups and network ACLs.  
- Deploy and connect **EC2 instances** across public and private networks.  
- Build and validate **VPC peering connections** for cross-network communication.  
- Monitor network traffic with **VPC Flow Logs** and analyze data using CloudWatch Logs Insights.  
- Secure service connectivity with **S3 bucket policies and VPC endpoints**.  

---

### How to Explore

Each module folder contains:
- A **detailed README.md** explaining the project, tools used, and lessons learned.  
- **Architecture diagrams** showing resource layouts and traffic flows.  
- Screenshots and command outputs documenting the process step by step.  

Recommended order:  
1. Start with **VPC-Fundamentals** →  
2. Continue to **VPC-Operations** →  
3. Finish with **Advanced-VPC-Operations**  

---

### Project Architecture

This diagram provides a high-level overview of the entire VPC networking journey, from basic subnet setup to advanced logging and secure S3 access with VPC endpoints.

---

![Project Architecture](images/architecture-overview.png)

---
