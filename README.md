# aws-secure-multi-tier-vpc
Secure Multi-Tier AWS VPC Architecture

Author: Alex Friedman / Caelus Tech Solutions
Project Type: AWS Cloud Infrastructure | Networking | Security | High Availability Design
Environment: AWS Free Tier / Lab Environment

Project Overview

This project demonstrates the design and implementation of a secure multi-tier Virtual Private Cloud (VPC) architecture in Amazon Web Services (AWS). The environment was built to simulate a production-style network architecture using public and private subnets, controlled administrative access, and layered security through Security Groups and Route Tables.

The objective of this project was to improve hands-on knowledge of:

AWS networking
Secure system administration
Multi-tier cloud architecture
Access control and segmentation
Bastion host management
Private subnet design
NAT Gateway implementation
Infrastructure documentation

The environment separates internet-facing systems from backend resources to reduce attack surface and follow security best practices.

Architecture Overview

The architecture consists of:

Public Subnet (10.0.0.0/24)

Hosts internet-accessible resources:

Bastion Host
Secure administrative jump box
SSH access restricted to my public IP only
Web Server
Public-facing EC2 instance
HTTP/HTTPS enabled
SSH access only through Bastion Host
NAT Gateway
Allows outbound internet access for private resources
Prevents inbound internet exposure
Private Subnet (10.0.2.0/24)

Hosts protected backend systems:

Backend Server
No public IP address
Accessible only from the web server
Internet access restricted to outbound traffic via NAT Gateway
Security Design

Security was implemented using least privilege access principles.

Bastion Security Group

Purpose: Secure administrative access

Inbound:

SSH (22) → My public IP only (/32)

Outbound:

All traffic allowed
Web Server Security Group

Purpose: Public web access

Inbound:

HTTP (80) → Internet
HTTPS (443) → Internet
SSH (22) → Bastion Security Group only

Outbound:

All traffic allowed
Backend Security Group

Purpose: Internal application layer

Inbound:

SSH (22) → Web Server Security Group only

Outbound:

All traffic allowed

This configuration prevents direct internet exposure of internal systems.

Networking Components
Internet Gateway

Provides public internet access to public subnet resources.

NAT Gateway

Allows private subnet instances to:

Install updates
Download packages
Reach external services

Without exposing internal servers to inbound internet traffic.

Route Tables

Public Route Table

Local traffic → VPC
0.0.0.0/0 → Internet Gateway

Private Route Table

Local traffic → VPC
0.0.0.0/0 → NAT Gateway
Architecture Diagram

(Insert your VPC diagram here)

Skills Demonstrated
AWS Services
VPC
EC2
Internet Gateway
NAT Gateway
Security Groups
Route Tables
Elastic IPs
Cloud Concepts
Network segmentation
Secure access design
Public vs private subnets
Bastion host architecture
Defense in depth
Least privilege security
Layered infrastructure
Technical Skills
SSH administration
Security hardening
Cloud architecture documentation
Troubleshooting network routing
Infrastructure planning
Future Improvements

Potential production enhancements include:

Multi-AZ deployment for high availability
Application Load Balancer (ALB)
Auto Scaling Groups
Private database subnet
AWS Systems Manager Session Manager
Infrastructure as Code using Terraform or CloudFormation
Centralized logging with CloudWatch
AWS WAF and Shield protection

	




