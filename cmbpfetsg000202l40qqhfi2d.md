---
title: "AWS Three-Tier Architecture"
seoTitle: "AWS Three-Tier Architecture Guide"
seoDescription: "Guide on AWS three-tier architecture with React, Spring Boot, and Amazon Aurora for scalable, secure applications. Learn technology roles and layers"
datePublished: Mon Jun 09 2025 18:29:16 GMT+0000 (Coordinated Universal Time)
cuid: cmbpfetsg000202l40qqhfi2d
slug: aws-three-tier-architecture
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1749493591274/d71735c8-bf83-40e5-a57f-074edde06e0f.webp
tags: aws, java, javascript, technology, architecture, developer, devops, springboot, three-tier-architecture

---

## Introduction

Modern web applications are often built using a **three-tier architecture** that separates concerns into layers for scalability, maintainability, and security.

Combining technologies like **React** for frontend, **Spring Boot** for backend APIs, and **Amazon Aurora** for database storage, deployed on **AWS**, provides a powerful, scalable, and secure architecture.

![Cloud Architecture of a Web App in a 3-Tier Architecture Model with Regional and Zone Redundancy for Disaster Management | System Design Blog by Umer Farooq](https://miro.medium.com/v2/resize:fit:2000/1*FvYPVcjeotm4LvDCYEg80w.png align="left")

---

## 1\. Understanding the Three-Tier Architecture

Three-tier architecture divides an application into three layers, each with specific responsibilities:

| Tier | Purpose and Role | Example Technologies / Services |
| --- | --- | --- |
| **Presentation Tier** | User interface layer that interacts directly with users, rendering the UI and handling user events. | React (frontend framework), Node.js (development tooling), AWS S3 (static hosting), AWS CloudFront (CDN) |
| **Application Tier** | Contains business logic, processes requests, validates data, and communicates with the data layer. | Spring Boot microservices (Java-based REST APIs), hosted on AWS ECS/EC2 |
| **Data Tier** | Responsible for persistent data storage and management. Not directly accessible from frontend. | Amazon Aurora (MySQL/PostgreSQL-compatible managed database) |

---

## 2\. Technology Roles Explained

* **React:** A JavaScript library used to build dynamic, responsive single-page applications (SPAs). React apps run in the user’s browser and communicate with backend services.
    
* **Node.js:** Primarily used here for development and build processes (via tools like Vite or Webpack). In this architecture, Node.js typically is *not* the production backend.
    
* **Spring Boot:** A popular Java framework to build RESTful backend microservices, implementing business logic and providing APIs consumed by the frontend.
    
* **Amazon Aurora:** A highly available, managed relational database service on AWS, compatible with MySQL or PostgreSQL, providing performance and scalability.
    
* **AWS S3:** Object storage service for hosting React’s static files (JS, CSS, HTML).
    
* **AWS CloudFront:** A global CDN caching and delivering your frontend files from edge locations close to users worldwide, ensuring fast load times.
    
* **AWS ECS/EC2:** Infrastructure services hosting backend microservices; ECS runs containerized apps, EC2 provides virtual machines.
    

---

## 3\. AWS Networking and Security Concepts

* **Virtual Private Cloud (VPC):** An isolated virtual network within AWS, where your application infrastructure runs securely.
    
* **Subnets:**
    
    * **Public Subnet:** Has internet connectivity; hosts resources like Load Balancers and Jump Servers.
        
    * **Private Subnet:** No direct internet access; houses backend services and databases for security.
        
* **Security Groups:** Virtual firewalls controlling inbound/outbound traffic to AWS resources.
    
* **Jump Server (Bastion Host):** A secure, hardened server in a public subnet used to access backend servers in private subnets via SSH.
    

---

## 4\. How the Application Works: Step-by-Step Request Flow

---

### Step 1: User Enters Website URL & DNS Resolution via Route 53

* The user types the web app URL (e.g., [`https://www.amitsangwan-demo.com`](https://yourapp.com)) into their browser and presses Enter.
    
* The browser performs a **DNS lookup** to resolve the domain name into an IP address.
    
* The domain is managed by **AWS Route 53**, AWS’s DNS service, which responds with the IP address of your **CloudFront distribution** (or another relevant endpoint).
    
* This resolution directs the user’s browser to connect to the nearest CloudFront edge location.
    

---

### Step 2: Request Hits AWS CloudFront (Global CDN)

* CloudFront routes the request to the nearest **edge location** geographically.
    
* CloudFront checks if the requested static asset (React JS, CSS, HTML) is cached:
    
    * If yes, CloudFront instantly serves it to the user.
        
    * If not, it fetches the asset from the **origin server** (AWS S3 bucket) and caches it for future use.
        

---

### Step 3: Static React Files Loaded from AWS S3

* React app files stored in AWS S3 are delivered to CloudFront, then to the user.
    
* The user’s browser renders the React frontend UI.
    

---

### Step 4: User Interacts with React App — API Requests Triggered

* When the user performs actions requiring backend data (e.g., login, fetch data), React sends **REST API** calls.
    

---

### Step 5: Requests Reach Application Load Balancer (ALB)

* API calls hit the ALB hosted in a public subnet, which forwards them to healthy backend Spring Boot microservice instances running in private subnets.
    

---

### Step 6: Backend Processes API Requests

* Spring Boot services handle authentication, business logic, and data validation.
    
* If needed, they query or update data stored in Amazon Aurora.
    

---

### Step 7: Backend Communicates with Amazon Aurora Database

* The database is securely located in a private subnet, inaccessible from outside the VPC.
    
* Data is stored, retrieved, or updated based on backend logic.
    

---

### Step 8: Backend Sends Response Back to Frontend

* Processed data is sent back through the ALB to the React app.
    
* The frontend updates the UI with fresh data.
    

---

## 5\. Secure Management Access

* Backend servers do not have public IPs.
    
* Administrators connect via **Jump Server** (in public subnet) to securely SSH into backend servers in private subnets.
    
* AWS (SSM) Systems Session Manager can be an alternative for secure access without opening SSH ports.
    

---

# AWS VPC and Subnets Layout Visualisation

```plaintext
    [Internet User Request]
             │
             ▼
┌────────────────────────────┐
│          AWS Route 53       │  ← DNS resolves domain to CloudFront IP
└─────────────┬──────────────┘
              │
              ▼
┌────────────────────────────┐
│       AWS CloudFront        │  ← Global CDN caches React app files
│       (Edge Location)       │
└─────────────┬──────────────┘
              │
              ▼
┌────────────────────────────┐
│        AWS S3 Bucket        │  ← Origin for React static assets
└─────────────┬──────────────┘
              │
              ▼
┌────────────────────────────┐
│      User’s Browser         │  ← React app runs here, sends REST API calls
└─────────────┬──────────────┘
              │ REST API Request
              ▼
┌────────────────────────────┐
│          VPC Network        │
│                            │
│  ┌──────────────┐          │
│  │  Public Subnet │         │
│  │ (Internet-facing)│      │
│  │   ┌───────────┐│         │
│  │   │  ALB      ││  ← Routes API requests securely
│  │   └───────────┘│
│  │   ┌───────────┐│
│  │   │ Jump Server││  ← Bastion host for SSH access to private subnet
│  │   └───────────┘│
│  └──────────────┘          │
│           │                 │
│           │ Routes API calls│
│           ▼                 │
│  ┌──────────────┐          │
│  │ Private Subnet │         │
│  │  (No Internet) │         │
│  │   ┌───────────┐│         │
│  │   │ Microservices│        │
│  │   │  (Spring    │        │
│  │   │   Boot)    │        │
│  │   │  Auth, User,│        │
│  │   │  Order etc.)│        │
│  │   └─────┬─────┘│
│  │         │      │
│  │   ┌─────▼─────┐│
│  │   │ Aurora DB ││  ← Secure data storage
│  │   └───────────┘│
│  └──────────────┘          │
│                            │
└────────────────────────────┘
```

---

---

## 7\. Summary of Key Concepts

| Concept | Explanation |
| --- | --- |
| **Route 53** | AWS’s DNS service resolving domain names to IP addresses directing traffic to CloudFront or backend resources. |
| **CloudFront CDN** | Delivers cached frontend content worldwide from edge locations, improving speed and reducing load on origin. |
| **VPC & Subnets** | Isolates infrastructure; public subnets expose internet-facing services, private subnets protect backend and DB. |
| **Jump Server** | Secure access point for administrators to backend servers, preventing direct public access. |
| **REST API** | Interface between frontend and backend allowing communication via HTTP requests/responses. |
| **Spring Boot Microservices** | Modular backend services handling specific business functions. |
| **Amazon Aurora** | High-performance, managed database service providing durability and scalability. |

---

## Conclusion

This architecture is designed to be:

* **Secure** — isolating backend and database in private networks, controlled access through Jump Servers and security groups.
    
* **Scalable** — independent scaling of frontend (via CloudFront), backend (via ECS/EC2), and database (Aurora).
    
* **Performant** — fast global content delivery via CloudFront and Aurora’s optimized database engine.
    
* **Maintainable** — clear separation of concerns allows teams to work independently on frontend, backend, and data.