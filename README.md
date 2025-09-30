# AWS 3-Tier Web Application Architecture

This repository demonstrates the design and deployment of a scalable and secure **3-Tier Web Application Architecture** on AWS, following best practices for high availability, fault tolerance, and security.

## Architecture Overview

The architecture is divided into 3 layers:

1. **Web Tier** – Handles user-facing elements and distributes traffic efficiently using **Nginx**.
2. **Application Tier** – Processes business logic with **Node.js-based application servers**.
3. **Database Tier** – Manages data storage and retrieval securely and efficiently.

![Architecture Diagram](https://raw.githubusercontent.com/Bhattu-Sai-Praneeth/3-TIER-AWS/main/Architecture.svg)

## Prerequisites

- An AWS account with IAM user access.
- Familiarity with the AWS Management Console.
- Knowledge of **VPC, EC2, Auto Scaling Groups, Security Groups**.
- Command-line access to **AWS CLI**.

## Step-by-Step Setup

### 1. Create a Virtual Private Cloud (VPC)

- **CIDR Block:** `10.0.0.0/16`
- **Subnets:**
  - 2 Public Subnets (Web Tier)
  - 4 Private Subnets (2 for Application Tier, 2 for Database Tier)
- **Internet Gateway:** For public internet access.
- **Route Tables:**
  - Public Route Table: Routes traffic from public subnets to the internet.
  - Private Route Table: Routes traffic from private subnets to the internet via a NAT Gateway.

### 2. Set Up the Web Tier

- **Launch EC2 Instances:** Deploy Nginx on Amazon Linux 2 instances.
- **Auto Scaling Group:** Configure to automatically adjust the number of instances based on traffic.
- **Application Load Balancer (ALB):** Distribute incoming traffic across EC2 instances.

### 3. Configure the Application Tier

- **Launch EC2 Instances:** Deploy Node.js-based application servers in private subnets.
- **Security Groups:** Restrict inbound traffic to allow connections only from the Web Tier.

### 4. Set Up the Database Tier

- **Amazon RDS:** Deploy a database instance (e.g., MySQL or PostgreSQL) in private subnets.
- **Security Groups:** Restrict inbound traffic to allow connections only from the Application Tier.

### 5. Implement Security Best Practices

- **Network ACLs:** Control inbound and outbound traffic at the subnet level.
- **IAM Roles:** Assign proper permissions to EC2 instances for accessing other AWS services.
- **Security Groups:** Ensure least privilege access between tiers.

### 6. Enable High Availability and Fault Tolerance

- **Multi-AZ Deployment:** Distribute resources across multiple Availability Zones.
- **Auto Scaling:** Automatically scale resources in response to traffic changes.
- **Backup and Recovery:** Implement automated backups for RDS and EC2 instances.

## Key Benefits

- **Scalability:** Each tier can scale independently based on load.
- **Fault Tolerance:** Failures in one tier do not affect the others.
- **Security:** Subnet isolation and proper security groups improve overall security.
- **Maintainability:** Easier to manage and update individual components.

## Services Used

- **AWS Services:** EC2, VPC, Subnets, Security Groups, Auto Scaling, Application Load Balancer, RDS, IAM
- **Web Server:** Nginx
- **Application Server:** Node.js
- **Database:** MySQL
