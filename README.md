# AWS Cloud Infrastructure & Deployment Project

## 🚀 Project Overview

This repository contains a comprehensive set of tasks completed during my **AWS Cloud Internship Tasks**. The project demonstrates a full-cycle deployment—starting from a single EC2 instance to a highly available, auto-scaling, and cost-optimized infrastructure.

The core of this project is built around **Dockerized applications** running on **Amazon Web Services (AWS)**, following industry best practices for security, reliability, and cost-efficiency.

## 🛠️ Tech Stack & Services

* **Cloud Provider:** Amazon Web Services (AWS)
* **Compute:** EC2, Auto Scaling Groups (ASG), Launch Templates
* **Networking:** VPC, Route 53, Application Load Balancer (ALB), Elastic IP
* **Containerization:** Docker
* **DNS & Domains:** Hostinger (Domain Registrar), Route 53 (DNS Management)
* **Security:** IAM, Security Groups

## 📁 Repository Structure

| Folder | Task Description | Key AWS Services |
| --- | --- | --- |
| **[EC2 Deployment]()** | Launching EC2 and initializing the Docker runtime environment. | EC2, Docker |
| **[Application Access]()** | Mapping a custom domain to AWS using static IPs and DNS delegation. | Route 53, Elastic IP |
| **[Load Balancer & Auto Scaling]()** | Implementing high availability and CPU-based elasticity. | ALB, ASG, CloudWatch |
| **[Cost Optimization]()** | Strategies for maintaining a zero-cost infrastructure under Free Tier. | AWS Budgets, Right-sizing |
| **[Troubleshooting]()** | Documenting and resolving common cloud connectivity and container issues. | Logs, CLI Debugging |

## 🏗️ Global Architecture

The final infrastructure is designed to be **highly available**. Traffic enters through a custom domain (`nikhilesh.sbs`), is resolved by **Route 53**, and directed to an **Application Load Balancer**. The ALB then distributes the load to **Dockerized Nginx containers** managed by an **Auto Scaling Group** that expands or shrinks based on CPU demand.

## 🚀 Quick Start & Verification

If you are reviewing this project, you can verify the deployment by Reviewing the `architecture` and `PDF` in each folder for detailed diagrams.