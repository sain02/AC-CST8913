# LAB-3
# Cloud Migration Comparative Study

**Name:** Saizal Saini  
**Student Number:** 041168394   

---

## 1. On-Premises Architecture

The organization currently runs workloads in an **on-premises data center** with the following components:

- **Web Application (Monolith)** – Hosted on local servers.  
- **Database (SQL Server)** – Stored on a central SQL DB.  
- **File Server** – For document and media storage.  
- **Networking** – Switches, routers, firewall.  
- **Email Server** – On-premises Exchange server.  

![alt text](<Screenshot 2025-09-27 223352-1.png>)

---

## 2. Cloud Service Mapping

| On-Prem Component | Cloud Model | Notes |
|-------------------|-------------|-------|
| Web Application   | **IaaS** (initial lift & shift) → **PaaS** (refactor later) | Start with VMs, later App Services or Kubernetes. |
| Database (SQL)    | **PaaS** (Managed DB) | Azure SQL DB / RDS / Cloud SQL. |
| File Server       | **PaaS** (Object Storage) | Azure Blob / AWS S3 / GCP Cloud Storage. |
| Networking        | **IaaS** | VNet / VPC + VPN/ExpressRoute. |
| Email             | **SaaS** | Exchange Online / Gmail / Amazon WorkMail. |

---

## 3. Migration Plan (Phases 0–6)

### **Phase 0 – Assessment & Planning**
- Inventory all applications, DBs, and dependencies.  
- PoC small workloads in the cloud.  
- Document compliance & security requirements.  

### **Phase 1 – Foundation Setup**
- Configure Identity (AAD, IAM, Cloud IAM).  
- Create VNet/VPC and subnets.  
- Enable monitoring and cost alerts.  

### **Phase 2 – Storage & Email Migration**
- Migrate file server → Blob/S3/Cloud Storage.  
- Migrate email → SaaS provider.  

### **Phase 3 – Database Migration**
- Use DMS or backup & restore.  
- Validate schema & application connectivity.  

### **Phase 4 – Application Migration**
- Lift & shift to VMs (IaaS).  
- Plan refactoring → App Services / GKE / EKS (PaaS).  

### **Phase 5 – Cutover & Decommission**
- Switch DNS to cloud workloads.  
- Decommission old servers.  

### **Phase 6 – Optimization**
- Enable autoscaling, monitoring, and backups.  
- Cost optimization using reserved instances.  

---

## 4. Comparative Study (Azure / AWS / GCP)

| Service Type | **Azure** | **AWS** | **GCP** |
|--------------|-----------|---------|---------|
| IaaS Compute | Azure VMs | EC2 | Compute Engine |
| PaaS App     | App Services | Elastic Beanstalk | App Engine |
| DB PaaS      | Azure SQL | RDS | Cloud SQL |
| Storage      | Blob Storage | S3 | Cloud Storage |
| Networking   | VNet | VPC | VPC |
| SaaS Email   | Exchange Online | WorkMail | Gmail |

**Provider Strengths:**
- **Azure** → Strong Microsoft ecosystem integration.  
- **AWS** → Largest service catalog, global reach.  
- **GCP** → Best for analytics, ML, and cost-effective compute.  

---

## 5. Hybrid Migration Approach
- **Start:** Lift & Shift → IaaS for quick migration.  
- **Later:** Refactor → PaaS for scalability.  
- **Email & Productivity:** Move directly to SaaS.  
- **Networking:** Hybrid VPN/ExpressRoute until fully cloud-based.  

---

---
# THANKS
