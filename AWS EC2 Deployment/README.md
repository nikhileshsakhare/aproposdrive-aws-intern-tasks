# Task 3: AWS EC2 Deployment

## 📌 Objective

The goal of this task was to provision a cost-optimized cloud compute environment and prepare it for containerized applications. This serves as the foundation for the entire project infrastructure.

## 🏗️ Architecture Overview

* **Instance Type:** `t2.micro` (or `t3.micro`), selected for AWS Free Tier eligibility.
* **Operating System:** Amazon Linux 2023 / Ubuntu.
* **Security Group:** Configured with Inbound rules for:
* **SSH (Port 22):** For remote management.
* **HTTP (Port 80):** To allow web traffic to the Docker containers.

* **Runtime:** Docker Engine installed for container orchestration.
Refer to the pdf in this folder for the visual network flow.

## 🛠️ Implementation Steps

### 1. Instance Provisioning

Launched an EC2 instance within the Public Subnet of the default VPC. I ensured the "Auto-assign public IP" was enabled to allow external access.

### 2. Docker Installation & Configuration

Once the instance was running, I connected via SSH and executed the following to prepare the environment, use setup_commands file for reference.

### 3. Container Deployment

I deployed a sample Nginx web server to verify the port mapping and security group configurations.

---

## ✅ Verification

To confirm the deployment was successful, I performed the following checks:

1. **Process Check:** Ran `docker ps` to verify the container status is `Up`.
2. **Network Connectivity:** Accessed the instance's **Public IPv4** via a web browser.
3. **Log Inspection:** Verified container logs using `docker logs web-server`.

> **Note:** Screenshots of the successful Nginx welcome page and the EC2 console status are located in the `screenshots/` directory.

## 📂 Files in this Folder

* `task3_architecture`: Visual diagram of the EC2 and Docker setup.
* `setup-commands.txt`: A text file containing all commands executed during setup.
* `Screenshots/`: Visual proof of the running instance and container.
* `task3_deliverable_pdf`: A PDF file explaining all the steps in detail.