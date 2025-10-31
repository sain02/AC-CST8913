# Cloud Migration Project - ShopPro International (Lab 9)

### Submitted By- Saizal Saini <br> Student Number- 041168394

## Overview
**ShopPro International** is a global eCommerce company planning to migrate its on-premises infrastructure to **Microsoft Azure (Canada Central)**.  
The company operates across **North America, Europe, and Asia-Pacific**, serving millions of users with multiple services such as web front-end, back-end APIs, payment systems, databases, analytics, and machine learning workloads.

This report provides:
1. **Cost Estimate Report** – Detailed breakdown of migration, operational, and management costs.  
2. **Cost Optimization Strategy** – Recommendations for reducing expenses.  
3. **Future Growth & Budget Plan** – Three-year cost projection and optimization roadmap.

---

## Section-1 Cost Estimate Report

### Migration Cost (One-time)
These are the initial expenses for moving data, databases, and applications from on-premises to Azure.

| Component | Description | Estimated Cost (CAD) | Notes |
|------------|--------------|----------------------|-------|
| **Database Migration** | Azure Database Migration Service for SQL + NoSQL | **$1,200** | 30 TB total data transfer |
| **VM Migration** | Azure Migrate to lift and shift 50+ VMs | **$800** | Temporary compute & replication |
| **Data Transfer** | Uploading on-prem data to Azure Blob Storage | **$300** | 30 TB at ~$0.01/GB |
| **Testing & Validation** | Verification of migration and app reconfiguration | **$500** | Includes pilot tests and downtime |
| **Total Migration Cost** |  | **≈ $2,800 CAD (One-Time)** |  |

**Explanation:**  
Azure Migrate and Database Migration Service ensure smooth transition with minimal downtime. The one-time migration cost mainly covers transfer bandwidth and resource validation.

---

### Operational Cost (Monthly)
These are recurring monthly expenses for running infrastructure and applications in Azure.

| Component | Description | Monthly Cost (CAD) | Notes |
|------------|-------------|--------------------|-------|
| **Web Front-End** | 30 VMs (10 per region) with Load Balancer & CDN | **$2,400** | High availability setup |
| **API Back-End Services** | 20 VMs hosting 50 microservices | **$1,800** | Autoscaling enabled |
| **Payment Processing** | 6 PCI-compliant secure VMs | **$1,200** | Includes encryption and Key Vault |
| **Database Layer** | SQL DB (5TB), NoSQL DB (10TB), Data Warehouse (15TB) | **$3,500** | Azure SQL + Cosmos DB + Synapse |
| **Analytics & ML** | GPU VMs for training and batch jobs | **$900** | Runs on-demand |
| **Storage & Backup** | Geo-redundant storage (30 TB total) | **$600** | RA-GRS storage type |
| **Networking** | ExpressRoute + regional bandwidth | **$400** | Multi-region connectivity |
| **Total Operational Cost** |  | **≈ $10,800/month** |  |

**Explanation:**  
Auto-scaling optimizes compute resources based on traffic demand. Using **Azure Synapse** and **Cosmos DB** provides scalability for analytics and real-time data.

---

### Management Cost (Monthly)
Management tools ensure uptime, security, and cost visibility.

| Service | Description | Monthly Cost (CAD) |
|----------|--------------|--------------------|
| **Azure Monitor & Log Analytics** | Collects logs and performance data | **$200** |
| **Microsoft Defender for Cloud** | Security & compliance management | **$150** |
| **Azure Cost Management** | Budget alerts and cost analysis | **$50** |
| **Automation & Tagging** | Auto-shutdown non-peak resources | **$100** |
| **Total Management Cost** |  | **≈ $500/month** |

**Explanation:**  
These services help maintain system health, detect threats early, and optimize spending through real-time monitoring.

---

### **Summary of Estimated Costs**

| Category | Description | Cost (CAD) |
|-----------|--------------|------------|
| **Migration Cost (One-time)** | Setup & data transfer | **$2,800** |
| **Operational Cost (Monthly)** | Running workloads | **$10,800** |
| **Management Cost (Monthly)** | Monitoring & security | **$500** |
| **Total Monthly Cost (Operational + Management)** |  | **≈ $11,300/month** |

---

## Section-2 Cost Optimization Strategy

| Optimization Method | Description | Potential Savings |
|----------------------|-------------|-------------------|
| **Reserved Instances (1-3 Years)** | Commit to long-term VM usage | **Up to 40%** |
| **Azure Hybrid Benefit** | Use existing Windows Server licenses | **15–20%** |
| **Auto-scaling Policies** | Scale backend services based on demand | **30% during off-peak** |
| **Spot Instances** | Use discounted VMs for ML batch jobs | **Up to 70%** |
| **Right-sizing** | Regularly review and downsize over-provisioned VMs | **10–15%** |
| **Auto-shutdown Policies** | Turn off dev/test VMs after hours | **5–10%** |
| **Azure Savings Plan** | Flexible commitment across VM types | **Up to 15%** |

**Explanation:**  
By mixing **reserved instances** for predictable workloads and **pay-as-you-go** for variable ones, ShopPro can balance flexibility with savings.  
Enabling **auto-scaling**, **auto-shutdown**, and **Hybrid Benefits** ensures long-term cost efficiency.

---

## 3. Future Growth and Budget Plan (3-Year Projection)

| Year | Projected Growth | Adjustments | Estimated Monthly Cost (CAD) |
|------|------------------|-------------|-------------------------------|
| **Year 1** | Base load | Initial deployment | **$11,300** |
| **Year 2** | +15% users | Add 10 VMs and scale DB storage | **$13,000** |
| **Year 3** | +30% users | Move backend to Azure Functions (serverless) | **$14,200** |

### Long-Term Optimization Recommendations
1. **Migrate APIs to Azure Kubernetes Service (AKS)** for containerized scaling.  
2. **Use Azure Functions (serverless)** for event-driven workloads to reduce idle compute costs.  
3. **Adopt Azure Data Lake + Synapse** for analytics to replace manual batch VMs.  
4. **Enable Tiered Blob Storage** – Move older data to “Cool” or “Archive” tiers.  
5. **Upgrade to newer VM families (D4as_v5, E4ds_v5)** for better cost/performance ratio.  

**Goal:** Keep growth cost under **+25% per year** while supporting 30% more users.

---

## Summary

| Category | Cost Type | Estimated Cost |
|-----------|------------|----------------|
| Migration | One-time | **$2,800** |
| Operations | Monthly | **$10,800** |
| Management | Monthly | **$500** |
| **Total Monthly (Operational + Management)** |  | **$11,300** |
| **Year 3 Projection** |  | **$14,200/month** |

**Estimated Annual Cost (Year 1):** ~ $135,600 CAD  
**Potential Savings (using optimizations):** 35–45% per year

---

## Tools Used
- **Azure Pricing Calculator** (Canada Central Region)  
- **Azure Migrate & Database Migration Service**  
- **Azure Monitor**, **Azure Cost Management**, **Microsoft Defender for Cloud**

---
## THANKS



