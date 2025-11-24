# Week 11 – Application Migration Lab  
### Name-Saizal Saini <br> Student Number-041168394
---
### Tailwind Traders - 3-Tier Application Migration to Azure

This document contains the full migration plan for Tailwind Traders’ on-premises 3-tier application. 

---

# Task 1 – Set Up Tooling for Discovery

## 1. Discovery Method (Agent-Based, Agentless, or Mix)
Tailwind Traders should use a **mix**:
- **Agentless** for VMware VMs (WEB01, WEB02, APP01)
- **Agent-based** for the physical SQL server (SQL01)

This gives complete performance, dependency, and SQL discovery data.

## 2. Number of Appliances Needed
Tailwind needs **1 Azure Migrate appliance** because:
- All servers are in the same datacenter.
- One appliance supports both VMware discovery and agent-based SQL discovery.

## 3. Required Credentials

| Purpose | Credentials Required |
|---------|----------------------|
| Software Inventory | Domain admin or local admin (Windows) |
| SQL Discovery | SQL login with `VIEW SERVER STATE` + `CONNECT ANY DATABASE` |
| Dependency Mapping | Windows admin credentials or read-only credentials |

## 4. Best Practices While Running Discovery
1. Run discovery for **2-4 weeks** to get full traffic patterns.  
2. Ensure **port 443 outbound** from the appliance to Azure is open.  
3. Make sure **time sync** is correct on VMware hosts and servers.

---

# Task 2 – Assessment Planning

## 1. Assessment Type
Tailwind should choose **Production** because the application is live and important.

## 2. Region & Performance Duration
- **Azure Region:** East US 2  
- **Performance Duration:** **30 days** (captures normal + weekend usage)

## 3. Sizing Method
Use **Performance-based sizing**, not on-prem VM size because:
- On-prem VMs may be oversized or undersized.
- Azure sizing should be based on real CPU, RAM, disk, and network usage.
- Reduces cost and improves performance.

## 4. Comfort Factor, Pricing & Licensing
- **Comfort Factor:** 1.2 (20% safety buffer)
- **Pricing Model:** 3-year Reserved Instance (cost savings)
- **Licensing Model:** Azure Hybrid Benefit (reuse Windows + SQL licenses)

---

# Task 3 – Dependency Analysis

## 1. Application Components
- **WEB01, WEB02** – Web frontend servers  
- **APP01** – Application / API server  
- **SQL01** – SQL Server 2017  
- **LB01** – Internal load balancer  

## 2. At Least 8 Dependencies

| Component Source | Destination | Dependency |
|------------------|-------------|------------|
| WEB → APP | Port 80/443 | API communication |
| APP → SQL | Port 1433 | Database queries |
| WEB → LB01 | Load balancing | Frontend traffic routing |
| APP → LDAP | Port 389 | Authentication |
| SQL → Backup Server | SMB | Nightly backups |
| APP → Email Server | SMTP 25/587 | Notification services |
| WEB/API → External API | HTTPS | Third-party services |
| SQL → Monitoring Tools | WMI | Performance and alerts |

## 3. Noise to Filter Out
- DNS lookups  
- NTP time sync  
- ARP / broadcast traffic  
- Antivirus update traffic  

## 4. Business Requirements

| Requirement | Detail |
|------------|--------|
| Business Criticality | High - core internal application |
| Uptime | 99.9% |
| Downtime Window | Strict 1-hour downtime allowed |
| Data Classification | Sensitive internal data |
| Licensing Needs | SQL 2017 Standard, Windows Server licenses |
| Patching | Monthly updates |
| Firewall/IP | Static IPs required, controlled port access |

---

# Task 4 – Validate Assessment Results with Application Owner

## 1. Recommended VM Sizes

| Server | Azure VM Size |
|--------|----------------|
| WEB01 / WEB02 | D2s_v5 |
| APP01 | D4s_v5 |
| SQL01 | E8ds_v5 |

## 2. Components to Replace or Optimize in Azure
- Replace **LB01** with **Azure Load Balancer (internal)**  
- SQL Server options:
  - Lift-and-shift to Azure VM  
  - Migrate to **Azure SQL Managed Instance**  
  - Or modernize to **Azure SQL Database**

## 3. Dependency Validation
- Confirm all WEB → APP → SQL communications  
- Validate external API connections  
- Verify backup traffic requirements  

## 4. SLA & Downtime Check
- Azure VM with Availability Zones = up to **99.99%**  
- App owner agrees migration can fit the **1-hour window**  
- Full testing supported before cutover  

## 5. SQL Migration Options Summary

| Option | Pros | Cons |
|--------|------|------|
| **Rehost (Lift & Shift)** | Fast, minimal changes | Full VM maintenance needed |
| **Azure SQL Managed Instance** | No patching, automated backups | Some features may differ |
| **Azure SQL Database** | Lowest maintenance | Not suitable for apps requiring full SQL Server control |

---

# Task 5 – Migration Plan (Runbook)

## A. Pre-Migration Steps
- Run full discovery (30 days)  
- Confirm VM sizes  
- Review dependency findings  
- Prepare Azure networking + subnets  
- Deploy Azure Load Balancer  
- Enable Azure Migrate replication for servers  

---

## B. Migration Steps

### Wave 1 (Web Tier)
1. Replicate WEB01 and WEB02  
2. Perform test migration  
3. Validate website loading  
4. Schedule cutover  
5. Shut down on-prem web servers  
6. Complete migration  
7. Add to Azure Load Balancer pool  

### Wave 2 (App Tier)
1. Replicate APP01  
2. Test migrate  
3. Validate API endpoints  
4. Cutover to Azure  

### Wave 3 (SQL Tier)
1. Back up SQL  
2. Enable replication  
3. Stop on-prem SQL jobs  
4. Wait for final sync  
5. Cutover SQL01 to Azure  
6. Update connection strings  

---

## C. DNS Updates
- Update internal DNS entries  
- Update any public-facing records  
- Confirm DNS TTL reduction before cutover  

---

## D. Connection String Changes
- Update APP01 to point to SQL in Azure  
- Update WEB servers if APP01 IP changes  

---

## E. Load Balancer Considerations
- Create internal Azure Load Balancer  
- Configure health probes  
- Add WEB01/WEB02 to backend pool  

---

## F. SQL Considerations
- Enable automated backups  
- Enable encryption (TDE)  
- Set up monitoring and alerts  

---

## G. Post-Migration Validation Checklist
- Website loads successfully  
- API functions working  
- SQL queries running normally  
- DNS resolves correctly  
- Firewall rules verified  
- Backups functioning  
- Monitoring enabled  

---

## H. Back-Out Plan
If migration fails:
- Point DNS back to on-prem servers  
- Restart SQL and APP01 on-prem  
- Shut down Azure VMs  
- Restore SQL backup if needed  
- Re-enable old firewall rules  

---

# Task 6 – Migration Waves

## Final Migration Waves

| Wave | Servers | Reason |
|------|---------|--------|
| **Wave 1** | WEB01, WEB02 | Stateless, very easy rollback |
| **Wave 2** | APP01 | Depends on web tier |
| **Wave 3** | SQL01 | Highest risk, needs careful downtime management |

---

---
### THANKS
