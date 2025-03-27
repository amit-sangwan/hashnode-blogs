---
title: "IAM, EC2, and EC2 Instance Storage"
seoDescription: "Learn about AWS IAM, EC2, and instance storage options including EBS, EFS, and best practices for managing security and backups"
datePublished: Wed Mar 26 2025 15:35:27 GMT+0000 (Coordinated Universal Time)
cuid: cm8q36etm000509jydpjw7dkf
slug: iam-ec2-and-ec2-instance-storage
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1743002715933/85d84621-b091-436b-8faf-d24556043ba8.jpeg
tags: aws

---

[  
](https://hashnode.com/@amit-sangwan)**Identity and Access Management (IAM)**

### ✅ **1\. What is IAM?**

AWS Identity and Access Management (**IAM**) is a global AWS service that allows you to securely control access to AWS services and resources.

### 🔥 **2\. Key IAM Components**

✅ **IAM Users:**

* Individual AWS accounts with unique credentials.
    
* Can access AWS via **console, CLI, or SDK**.
    
* Assigned specific permissions using **policies**.
    

✅ **IAM Groups:**

* Collections of IAM users with shared permissions.
    
* Easier management by applying policies at the group level.
    

✅ **IAM Roles:**

* **Temporary permissions** for AWS services or users.
    
* Used for EC2 instances, Lambda functions, and cross-account access.
    

✅ **IAM Policies:**

* JSON documents defining **permissions**.
    
* Example:
    

```bash
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "s3:ListBucket",
            "Resource": "*"
        }
    ]
}
```

✅ **IAM Best Practices:**

* **Enable MFA** (Multi-Factor Authentication) for added security.
    
* Use **IAM roles** for applications running on EC2 instances.
    
* Follow the **least privilege principle**.
    
* Rotate access keys regularly.
    

---

## ⚙️ **Amazon Elastic Compute Cloud (EC2)**

### 🔥 **1\. What is Amazon EC2?**

Amazon EC2 (**Elastic Compute Cloud**) provides resizable compute capacity in the AWS cloud. It offers **virtual servers** (instances) to run applications.

### ✅ **2\. EC2 Instance Types**

✅ **General Purpose:** Balanced compute, memory, and networking.

* Example: `t2.micro` (Free tier eligible).
    

✅ **Compute Optimized:** For CPU-intensive tasks.

* Example: `c5.4xlarge`.
    

✅ **Memory Optimized:** For memory-intensive applications.

* Example: `r5.large`.
    

✅ **Storage Optimized:** High I/O performance.

* Example: `i3.8xlarge`.
    

### 🔥 **3\. EC2 Purchasing Options**

✅ **On-Demand:**

* Pay as you go.
    
* Ideal for **short-term workloads**.
    

✅ **Reserved Instances:**

* 1 to 3-year commitment.
    
* Up to **72% discount** over On-Demand.
    

✅ **Spot Instances:**

* Uses spare AWS capacity.
    
* Up to **90% discount**, but can be terminated anytime.
    

✅ **Dedicated Hosts:**

* Physical servers dedicated to your use.
    
* Ideal for **compliance and licensing**.
    

✅ **Capacity Reservation:**

* Reserve compute capacity in a specific **AZ**.
    
* No discount, pay full On-Demand rate.
    

### 🔥 **4\. EC2 Security Groups**

* **Acts as a firewall** for your instances.
    
* Controls inbound and outbound traffic.
    
* Only **allow rules** are permitted.
    

✅ **Common Ports:**

* `22`: SSH (Linux access).
    
* `80`: HTTP.
    
* `443`: HTTPS.
    
* `3389`: RDP (Windows remote access).
    

### 🔥 **5\. AMI (Amazon Machine Image)**

**AMI** is a pre-configured template containing OS, application server, and applications.

✅ **AMI Features:**

* **Faster boot time** (pre-packaged software).
    
* Can be **copied across regions**.
    

✅ **AMI Types:**

* **Public AMI:** AWS-provided images.
    
* **Private AMI:** Your custom AMI.
    
* **Marketplace AMI:** Third-party images.
    

✅ **AMI Creation Process:**

1. Launch and customize an EC2 instance.
    
2. Stop the instance for data integrity.
    
3. **Create AMI** (includes EBS snapshot).
    
4. Use AMI to launch instances.
    

✅ **EC2 Image Builder:**

* Automates AMI creation and testing.
    
* **Regional service**.
    
* Can be scheduled (weekly, monthly).
    
* **Free service** (only underlying resources are billed).
    

---

## 💾 **EC2 Instance Storage**

### ✅ **1\. EBS (Elastic Block Store)**

**EBS Volumes** are network-attached storage drives used with EC2 instances. They provide **persistent storage** even after the instance is terminated.

✅ **EBS Features:**

* **Network drive** (not physically attached).
    
* **Bound to a specific AZ**.
    
* Can be detached and attached to another instance quickly.
    
* **Provisioned capacity:** Size in GBs and IOPS (Input/Output Operations Per Second).
    
* **Billed** for the entire provisioned capacity.
    

✅ **EBS Example:**

```bash
AZ1: EBS → Instance A  
AZ2: EBS Snapshot → Move to AZ2 → Attach to Instance B
```

✅ **EBS Delete on Termination:**

* **Root volume** deleted by default on termination.
    
* Additional volumes are **not deleted** by default.
    
* You can modify this setting to **preserve data** after termination.
    

✅ **EBS Snapshots:**

* **Point-in-time backup** of an EBS volume.
    
* Can be created without detaching the volume (recommended).
    
* Can be **moved across AZs or regions**.
    

✅ **EBS Snapshot Archive:**

* **75% cheaper** storage tier.
    
* Restores take **24-72 hours**.
    

✅ **Recycle Bin for EBS Snapshots:**

* Retains deleted snapshots.
    
* **Retention period:** 1 day to 1 year.
    

### 🔥 **2\. EC2 Instance Store**

* **High-performance hardware disk** attached directly to EC2.
    
* Better **I/O performance** than EBS.
    
* **Data loss** occurs if the instance is stopped or terminated.
    
* Ideal for:
    
    * Cache/buffer storage.
        
    * Temporary data.
        
* **User-managed** backups and replication.
    

### 🔥 **3\. EFS (Elastic File System)**

* **Managed NFS** that can be mounted on **100s of EC2 instances**.
    
* **Multi-AZ** architecture.
    
* Highly scalable and available.
    
* **Pay-per-use** pricing model.
    

✅ **EFS Infrequent Access (EFS-IA):**

* Storage tier for **rarely accessed files**.
    
* **92% lower cost** than standard EFS.
    
* Automatically moves files based on last access time.
    
* Lifecycle policies to optimize costs.
    

---

## 🔥 **Shared Responsibility Model**

✅ **AWS Responsibilities:**

* **Infrastructure Security:** Global security, physical hardware, and availability.
    
* **Data Center Operations:** Redundancy, uptime, and failover.
    
* **Networking:** Isolated VPC, firewall configurations, and DDoS protection.
    

✅ **User Responsibilities:**

* **IAM Management:** User roles, permissions, and MFA.
    
* **OS Patching and Updates:** Keeping instances secure and updated.
    
* **Data Encryption:** Encrypting data at rest and in transit.
    
* **Backup and Recovery:** Managing EBS snapshots and EFS backups.
    

---

## ✅ **Key Takeaways**

1. **IAM:** Secure access control with **users, groups, roles, and policies**.
    
2. **EC2:** Scalable virtual servers with various pricing models.
    
3. **EBS:** Network-attached, persistent storage with **snapshots and backups**.
    
4. **EFS:** Scalable, multi-instance file storage.
    
5. **FSx:** High-performance file systems for specific workloads.