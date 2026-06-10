# Secure Multi-Tier AWS VPC Architecture

## Project Overview

This project demonstrates the design and implementation of a **secure multi-tier Virtual Private Cloud (VPC)** architecture in Amazon Web Services (AWS).

The environment was built to simulate a **production-style network architecture** using:

- Public and private subnets
- Controlled administrative access
- Security group segmentation
- NAT Gateway for secure outbound traffic
- Bastion host access control

The objective of this project was to improve hands-on knowledge of:

- AWS Networking
- Secure System Administration
- Multi-Tier Cloud Architecture
- Access Control and Segmentation
- Private Subnet Design
- NAT Gateway Implementation
- Infrastructure Documentation

---

## Architecture Overview

### Public Subnet (10.0.0.0/24)

Hosts internet-facing resources:

#### Bastion Host
- Secure SSH jump box
- SSH access restricted to **my public IP only**

#### Web Server
- Public-facing EC2 instance
- HTTP (80) and HTTPS (443) enabled
- SSH access only through Bastion Host

#### NAT Gateway
- Provides outbound internet access for private resources
- Prevents inbound internet exposure

---

### Private Subnet (10.0.2.0/24)

Hosts protected backend resources:

#### Backend Server
- No public IP address
- Accessible only from the Web Server
- Outbound internet access via NAT Gateway

---

## Security Design

### Bastion Security Group

**Purpose:** Secure administrative access

**Inbound**
- SSH (22) → My Public IP only (/32)

**Outbound**
- All traffic allowed

---

### Web Server Security Group

**Purpose:** Public web access

**Inbound**
- HTTP (80) → Internet
- HTTPS (443) → Internet
- SSH (22) → Bastion Security Group only

**Outbound**
- All traffic allowed

---

### Backend Security Group

**Purpose:** Internal application layer

**Inbound**
- SSH (22) → Web Server Security Group only

**Outbound**
- All traffic allowed

This configuration prevents direct internet exposure of internal systems.

---

## Route Tables

### Public Route Table
- Local Traffic → VPC
- `0.0.0.0/0` → Internet Gateway

### Private Route Table
- Local Traffic → VPC
- `0.0.0.0/0` → NAT Gateway

---

## AWS Services Used

- VPC
- EC2
- Security Groups
- Route Tables
- Internet Gateway
- NAT Gateway
- Elastic IP

---

## Skills Demonstrated

### Cloud Concepts
- Network Segmentation
- Defense in Depth
- Least Privilege Security
- Public vs Private Architecture
- Secure Administrative Access

### Technical Skills
- SSH Administration
- Security Hardening
- Network Routing
- Infrastructure Documentation
- AWS Troubleshooting

---

## Future Improvements

Potential production enhancements:

- Multi-AZ deployment
- Application Load Balancer (ALB)
- Auto Scaling Groups
- Private Database Tier
- AWS Systems Manager Session Manager
- Terraform Infrastructure as Code
- CloudWatch Monitoring
- AWS WAF & Shield

---

