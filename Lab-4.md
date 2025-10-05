# LAB-4 Design Rehosting Migration V2
Name- Saizal Saini <br>
Subject- Cloud Migration <br>
Student Number- 041168394

# High-Level Design: Lift-and-Shift Migration

**App:** Node.js WebServerVM + SQL Server VM → **AKS (containers)** + **Azure Managed SQL**  

---

## Q1 — Solution Diagram (Target Architecture)
![alt text](<Screenshot 2025-10-05 134338.png>)


## Q2-Target Architecture (High-Level Description)

**Web Tier**: Node.js app is containerized and deployed to Azure Kubernetes Service (AKS). AKS provides orchestration, automatic restart, horizontal scaling, and native integration with Azure networking and load-balancing.

**Database Tier**: SQL Server is migrated to Azure SQL Managed Instance or Azure SQL Database (depending on feature parity needs). This removes VM management, offers automated backups, high availability (built-in HA), and point-in-time restore.

**Supporting Services**: Use Azure Container Registry (ACR) to store container images, Azure Load Balancer / Application Gateway (or Front Door) to expose the app, and Azure Monitor / Log Analytics for observability.

**Availability & Scalability**: AKS configured across multiple availability zones with node pools and pod replica sets ensures the web tier tolerates zone/node failures. Azure SQL Managed Instance provides SLA-backed high availability for the database.

## Q3- Migration Steps (Concise and Ordered)

### 1. Containerization of Web Application
- First, we take the existing Node.js web application from the WebServerVM.  
- Then, we create a Docker image of this application by writing a simple Dockerfile.  
- The Docker image packages the app and all its dependencies so it can run anywhere.  
- This image is tested locally to make sure it works properly.  
- After testing, the image is pushed to **Azure Container Registry (ACR)** so it can be used by Azure services.

### 2. Migration of Database to Managed SQL Service
- Next, we take the SQL Server database from the SQLVM.  
- We use Azure tools like **Azure Database Migration Service (DMS)** to move the data to **Azure SQL Database**, a fully managed cloud service.  
- All data, tables, and stored procedures are verified after migration.  
- Connection strings in the web application are updated to point to the new managed SQL Database.

### 3. Configuration of Kubernetes Cluster for High Availability
- We create an **Azure Kubernetes Service (AKS)** cluster to run the Dockerized web app.  
- The AKS cluster is deployed with multiple nodes to ensure high availability (so the app keeps running even if one node fails).  
- We deploy the web application container to AKS using Kubernetes manifests (like deployment and service files).  
- Load balancing is configured so user traffic is evenly distributed across multiple pods.  
- Auto-scaling is enabled to automatically handle more traffic when needed.  
- Finally, we test the setup to confirm the application works smoothly and can handle up to 6 hours of downtime during migration.

### Final Outcome
After completing these steps:
- The Node.js web app runs in containers managed by AKS.  
- The database runs on Azure’s managed SQL service.  
- The whole system is scalable, reliable, and easier to maintain in the cloud.

---
---
## THANKS
