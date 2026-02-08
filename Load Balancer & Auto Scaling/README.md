# Task 5: Load Balancing & Auto Scaling

## 📌 Objective

The goal of this task was to ensure the application is highly available and can handle fluctuating traffic. By implementing an Application Load Balancer (ALB) and an Auto Scaling Group (ASG), the infrastructure can now automatically detect instance failures and scale resources based on real-time CPU demand.

## 🏗️ Architecture Overview

* **Application Load Balancer (ALB):** Acts as the single point of contact for clients, distributing incoming traffic across multiple EC2 instances in different Availability Zones.
* **Auto Scaling Group (ASG):** Manages a dynamic collection of EC2 instances, ensuring the "Desired Capacity" is maintained.
* **Launch Template:** A saved configuration (AMI, Instance Type, Key Pair, Security Group) used by the ASG to provision new instances.
* **Target Group:** Routes requests from the Load Balancer to the healthy instances managed by the ASG.
* **Scaling Policy:** A target tracking policy that maintains average CPU utilization at **50%**.

Refer to `task5_architecture` for the visual layout of the ALB and ASG integration.

## 🛠️ Implementation Steps

### 1. Launch Template Creation

Created a template named `web-app-template` to automate instance deployment.

* **AMI:** Amazon Linux 2023.
* **User Data Script:** Automated the installation of Docker and started the Nginx container upon boot to ensure new instances are immediately ready to serve traffic.

### 2. Target Group & ALB Configuration

* Created a **Target Group** on Port 80 with health checks pointing to `/`.
* Provisioned an **Internet-Facing ALB** across multiple Availability Zones to ensure high availability.
* Configured an HTTP Listener on Port 80 to forward traffic to the Target Group.

### 3. Auto Scaling Group (ASG) Setup

* Attached the ASG to the existing Load Balancer and Target Group.
* **Capacity Settings:**
* **Minimum:** 1
* **Desired:** 1
* **Maximum:** 3

* **Health Check Type:** ELB (enabling the ASG to replace instances if the Load Balancer reports them as unhealthy).

### 4. Dynamic Scaling Policy

Implemented a **Target Tracking Scaling Policy**:

* **Metric:** Average CPU Utilization.
* **Target Value:** 50%.
* If the average CPU load exceeds 50%, the ASG automatically provisions a new instance.

## ✅ Verification & Stress Testing

To verify the elasticity of the system, I performed a manual stress test:

1. **Baseline:** Confirmed 1 instance was running and healthy.
2. **Observation:** Monitored CloudWatch metrics. Once CPU exceeded the 50% threshold, the ASG successfully launched a second instance to distribute the load.

## 📂 Files in this Folder

* `task3_architecture`: Diagram showing the ALB, Target Group, and ASG across multiple AZs.
* `user-data.sh`: The script used in the Launch Template for automation.
* `screenshots/`: ALB DNS name loading the application.
* `task5_deliverable_pdf`: A PDF file explaining all the steps in detail.