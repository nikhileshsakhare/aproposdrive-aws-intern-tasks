# Task 4: Application Access

## 📌 Objective

The goal of this task was to make the application accessible via a stable, user-friendly URL. This involved configuring static networking (Elastic IP) and managing DNS records to map the custom domain `nikhilesh.sbs` to the AWS infrastructure.

## 🏗️ Architecture Overview

* **Static Networking:** **Elastic IP (EIP)** was allocated to ensure the public IP address remains constant even if the instance is stopped or restarted.
* **DNS Management:** **Amazon Route 53** was used as the DNS service to manage Hosted Zones and records.
* **Domain Registrar:** **Hostinger**, where the domain name was purchased and the Name Servers (NS) were delegated to AWS.
* **Protocol:** **HTTP (Port 80)** traffic flow from the client browser to the EC2 instance.

Refer to `task4_architecture` for the detailed flow from the Client to the Nginx container.

## 🛠️ Implementation Steps

### 1. Elastic IP Allocation

Standard EC2 public IPs are dynamic. To prevent DNS breakage, I performed the following:

1. Allocated an **Elastic IP** in the EC2 Dashboard.
2. Associated the Elastic IP with the running **Nginx EC2 instance**.
3. Verified connectivity using the new static IP address.

### 2. Route 53 Hosted Zone Setup

1. Created a **Public Hosted Zone** in Route 53 for `nikhilesh.sbs`.
2. AWS generated four unique **Name Servers (NS)** for the zone.

### 3. DNS Delegation (Hostinger Integration)

To give AWS control over the domain's traffic:

1. Logged into the **Hostinger Control Panel**.
2. Updated the **Nameservers** by replacing Hostinger’s defaults with the four NS records provided by Route 53.

### 4. Creating the "A Record"

1. Inside the Route 53 Hosted Zone, created a new **Record Set**.
2. **Record Type:** `A - IPv4 address`.
3. **Value:** Pointed directly to the **Elastic IP** allocated in Step 1.

## ✅ Verification

1. **Propagation Check:** Used `dig nikhilesh.sbs` and online tools (like DNSChecker) to verify that the domain points to the Elastic IP globally.
2. **Browser Access:** Successfully loaded the Nginx "Welcome" page by navigating to `http://nikhilesh.sbs`.
3. **Persistence Test:** Restarted the EC2 instance to ensure the Elastic IP remained attached and the domain link stayed active.

## 📂 Files in this Folder

* `task4_architecture`: Diagram showing the connection between Hostinger, Route 53, and the EC2 Instance.
* `Screenshots/`: Visual proof of Successful browser access via the custom domain.
* `task4_deliverable_pdf`: A PDF file explaining all the steps in detail.