# AWS Down Server Recovery

## Overview

This project simulates a real-world cloud operations scenario where a production web server becomes unavailable due to infrastructure configuration issues. The objective was to deploy a secure AWS environment, restore application availability, and implement monitoring and alerting to proactively detect future outages.

This project was completed using the AWS Management Console and will later be recreated using Terraform as an Infrastructure as Code (IaC) implementation.

---

## Business Scenario

A company hosts a customer-facing web application on an Amazon EC2 instance. After deployment, users are unable to access the application from the internet.

As the Cloud Engineer, my responsibilities included:

- Building the required AWS networking infrastructure
- Deploying and configuring the EC2 instance
- Securing administrative access
- Restoring public access to the web application
- Implementing monitoring and alerting
- Validating end-to-end connectivity
- Documenting the deployment for future automation

---

## Objectives

- Deploy a custom Amazon VPC
- Create and configure a public subnet
- Configure an Internet Gateway
- Configure Route Tables
- Launch an Amazon EC2 instance
- Configure Security Groups
- Connect using SSH
- Allocate and associate an Elastic IP
- Install and configure Nginx
- Configure Amazon SNS notifications
- Create Amazon CloudWatch alarms
- Verify public web access
- Test monitoring and alerting

---

## Architecture

**Architecture Diagram**

<img width="499" height="440" alt="diagram" src="https://github.com/user-attachments/assets/e3a0c30f-cf66-48b7-b061-2898e2ba1138" />

---

## AWS Services Used

| Service | Purpose |
|----------|----------|
| Amazon EC2 | Hosted the web server |
| Amazon VPC | Isolated network resources |
| Public Subnet | Allowed internet connectivity |
| Internet Gateway | Provided internet access |
| Route Table | Routed traffic to the Internet Gateway |
| Security Groups | Controlled inbound and outbound traffic |
| Elastic IP | Provided a static public IPv4 address for reliable access to the web server |
| Amazon CloudWatch | Monitored EC2 health and triggered alarms |
| Amazon SNS | Sent email notifications when alarms were triggered |

---

## Deployment Process

### Step 1 — Build the Network

- Created a custom VPC
- Created a public subnet
- Attached an Internet Gateway
- Configured Route Tables
  
<img width="1629" height="731" alt="1  VPC " src="https://github.com/user-attachments/assets/59c1783f-f4a4-4151-9098-0cb1c06c06e7" />

<img width="1652" height="524" alt="1  Subnet" src="https://github.com/user-attachments/assets/e24ce3f0-ab8c-4fac-a628-4a97789412ac" />

<img width="1645" height="369" alt="3 IGW" src="https://github.com/user-attachments/assets/b9b4f8d7-1fab-43cb-ac67-02f371ca8f2d" />

<img width="1645" height="500" alt="Public RT" src="https://github.com/user-attachments/assets/3c714cda-b635-429b-bae1-74dc29aaead4" />

<img width="1645" height="456" alt="Subnet Association" src="https://github.com/user-attachments/assets/4cbacfe4-cb59-4a7c-9057-b123d070e308" />

---

### Step 2 — Secure the Environment

Configured Security Group rules to allow:

- SSH (22)
- HTTP (80)

<img width="1642" height="508" alt="Security group" src="https://github.com/user-attachments/assets/7dfe7b74-08db-49b0-8ec8-2bac6df847b6" />

---

### Step 3 — Launch the EC2 Instance

- Launched an Amazon Linux EC2 instance
- Verified networking
- Connected securely using SSH

<img width="1642" height="156" alt="EC2" src="https://github.com/user-attachments/assets/7c739311-4a37-4b8b-8b47-e9c5ea95ddfe" />




<img width="1451" height="480" alt="Successful SSH Connection" src="https://github.com/user-attachments/assets/205e1508-a769-4a1e-afa5-b1806b38322d" />


---

### Step 4 — Allocate an Elastic IP

Allocated and associated an Elastic IP with the EC2 instance to provide a consistent public IP address.

This prevents the server’s public IP from changing after the instance is stopped and started.

<img width="1623" height="397" alt="Elastic IP" src="https://github.com/user-attachments/assets/1e50a69f-489f-47f4-9151-ed653fbf0b44" />

---

### Step 5 — Deploy the Web Server

Installed and configured Nginx.

- Updated packages
- Installed Nginx
- Started the service
- Enabled Nginx at boot
- Verified browser access

<img width="2249" height="1391" alt="Install nginx on server" src="https://github.com/user-attachments/assets/5be99813-5c77-456e-aa5d-0b4f58b848d5" />




<img width="1914" height="597" alt="Welcome to Nginx success" src="https://github.com/user-attachments/assets/6ea122f5-32b3-47c3-a76c-e8a1757fa471" />


---

### Step 6 — Configure Amazon SNS

Configured Amazon SNS to send infrastructure alerts.

- Created an SNS Topic
- Added an email subscription
- Confirmed the subscription

<img width="1636" height="526" alt="SNS" src="https://github.com/user-attachments/assets/0fcfa657-ecd9-4cd3-bad3-84db6a4abe48" />

---

### Step 7 — Configure Amazon CloudWatch

Created a CloudWatch alarm to monitor the EC2 instance.

- Selected the EC2 metric
- Configured the alarm threshold
- Defined evaluation periods
- Connected the alarm to Amazon SNS

<img width="1908" height="309" alt="CloudWatch alert" src="https://github.com/user-attachments/assets/27443057-248b-4de7-8a8b-be48b99229e7" />


<img width="1243" height="471" alt="CW Configs" src="https://github.com/user-attachments/assets/3329f223-5996-4214-b7b0-f0e227c25776" />


---

### Step 8 — Validate the Solution

Verified:

- SSH connectivity
- Internet connectivity
- Public HTTP access
- Nginx web server availability
- Elastic IP association
- Website access using the Elastic IP
- CloudWatch alarm state
- Amazon SNS email notifications
  
---

## Screenshots

### AWS Infrastructure

- VPC
- Public Subnet
- Internet Gateway
- Route Table
- Security Group
- EC2 Instance

### Monitoring

- Amazon SNS
- Amazon CloudWatch Alarm
- Alarm State
- Email Notification

### Validation

- SSH Session
- Nginx Running
- Browser Verification

---

## Troubleshooting

### Issue

The EC2 instance was reachable through SSH, but the web application was unavailable from the browser.

### Root Cause

The Nginx web server had not been installed and configured.

### Resolution

- Installed Nginx
- Started the service
- Enabled automatic startup
- Verified HTTP connectivity

The monitoring solution was then validated by confirming CloudWatch alarms successfully triggered Amazon SNS email notifications.

---

## Lessons Learned

This project reinforced key AWS cloud engineering concepts, including:

- VPC Architecture
- Public Networking
- Route Tables
- Internet Gateways
- Security Groups
- Linux Administration
- SSH Connectivity
- Web Server Deployment
- Elastic IP allocation and association
- Difference between dynamic public IPs and static public IPs
- Amazon CloudWatch Monitoring
- Amazon SNS Notifications
- Infrastructure Troubleshooting

The most valuable takeaway was understanding how networking, compute, monitoring, and alerting work together to maintain application availability in AWS.

---

## Future Improvements

- Rebuild the infrastructure using Terraform
- Automate deployment with GitHub Actions
- Containerize the application using Docker
- Deploy the application to Amazon EKS
- Add an Application Load Balancer
- Deploy across multiple Availability Zones
- Implement Auto Scaling

---

## Repository Structure

```text
aws-down-server-recovery/
│
├── README.md
├── diagrams/
├── screenshots/
├── terraform/
├── docs/
├── docker/
├── kubernetes/
└── .github/
    └── workflows/
```

---

## Author

**Theodore Bullock**

Cloud Engineering Portfolio

**LinkedIn:** https://www.linkedin.com/in/theodore-bullock-j
