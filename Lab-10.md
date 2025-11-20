# Lab-10: Zero Trust Azure Landing Zone Design  
CloudMed Solutions Inc.
### Name- Saizal Saini <br> Student Number-041168394
---

## 1. **Company Overview**

CloudMed Solutions is a healthcare technology provider that delivers cloud-based telemedicine and patient-management services to hospitals and clinics in Canada, the United States, and Europe. Their core platform, **MedConnect**, supports virtual care consultations, secure EMR handling, and AI-driven health analytics.

Because the organization processes highly sensitive medical information across multiple regions, its cloud environment must follow strict privacy and regulatory frameworks such as **HIPAA**, **GDPR**, and **PIPEDA**. To ensure compliance and protect critical workloads, CloudMed requires a **Zero Trust–aligned Azure Landing Zone** that emphasizes identity security, segmentation, and continuous monitoring.

---

## 2. **Governance and Identity Structure**

### **Management Group Hierarchy**


### **Governance Model**

- **Role-Based Access Control (RBAC):**  
  Clear separation of responsibilities:
  - **Admins:** platform and security operations  
  - **DevOps:** application deployments and CI/CD  
  - **Finance:** cost monitoring and billing insights  

- **Azure Policy Usage:**  
  - Mandatory resource tagging  
  - Restricting allowed Azure regions to *Canada Central* and *West Europe*  
  - Enforcing configuration standards (no public IPs, encrypted storage, approved SKUs)

- **Identity Security with Azure Entra ID:**  
  - Conditional Access policies requiring MFA  
  - Sign-in risk analysis and device-compliance checks  
  - Identity Protection alerts and automated remediation  

This governance approach ensures consistent, controlled, and compliant operations across all workloads.

---

## 3. **Network Architecture (Hub-and-Spoke)**

CloudMed follows a **Hub-and-Spoke network layout** to isolate critical workloads while still enabling secure communication when needed.

### **Hub Network Components**
- **Azure Firewall** – inspects traffic and enforces Zero Trust rules  
- **Azure Bastion** – provides browser-based, secure admin access without public IPs  
- **Private DNS Zones** – internal name resolution  
- **Log Analytics Workspace** – centralized monitoring and logs  

### **Spoke Network Workloads**
- **App Spoke:** web and mobile frontend services  
- **API Spoke:** backend microservices  
- **Data Spoke:** SQL databases and storage, accessible only via **Private Endpoints**  

### **Segmentation & Traffic Control**
- Subnets separated by function (App / API / DB / Management)  
- Only east-west traffic explicitly allowed through firewall policies  
- No workload has a public IP; everything uses Private Link  

This architecture supports Zero Trust by limiting network exposure and ensuring all communication is authenticated and inspected.

---

## 4. **Zero Trust Controls**

CloudMed’s design applies all three foundational Zero Trust principles:

### **1. Verify Explicitly**
- MFA and Conditional Access for every user  
- Identity-based authentication between services  
- Device compliance and sign-in risk used during authorization  

### **2. Least Privilege Access**
- Minimal RBAC assignments  
- Just-In-Time (JIT) administrator access through Privileged Identity Management  
- Segregation of duties across Platform, Production, and Development  

### **3. Assume Breach**
- Network segmentation restricting lateral movement  
- End-to-end data encryption (SQL TDE, Storage SSE, encrypted transit)  
- Centralized logging, threat detection, and automated alerts  

### **Specific Design Examples**
- **Azure Bastion** for secure admin access without exposing VMs  
- **Private Link** for Azure SQL and Storage  
- **Policy to block all public IP creation**  
- **Firewall DNAT removal** to prevent unsolicited inbound traffic  
- **Defender for Cloud** for threat detection and compliance scoring  

---

## 5. **Monitoring, Compliance, and Cost Controls**

### **Resource Monitoring**
- **Log Analytics Workspace** for metrics, logs, and telemetry  
- **Azure Monitor Alerts** for performance and security issues  
- **Defender for Cloud** for continuous assessment and threat protection  

### **Compliance Enforcement**
- Azure Policies ensure adherence to HIPAA, GDPR, and PIPEDA principles  
- Policy compliance dashboard for reporting and audit preparation  
- Regulatory compliance initiative assignment through Defender for Cloud  

### **Cost Management**
- Budgets set per environment (Production, Dev, Platform)  
- Alerts for budget thresholds  
- Tagging standards (Environment, Owner, CostCenter) to track spending  

---

## 6. Summary and Recommendations

The proposed Azure Landing Zone offers CloudMed a secure and structured foundation for operating healthcare workloads in the cloud. The design incorporates core Zero Trust principles—strong identity verification, least-privilege access controls, and network segmentation—to protect sensitive medical information. By using a Hub-and-Spoke network model, Private Endpoints, RBAC, Azure Policies, and continuous monitoring through Log Analytics and Defender for Cloud, the environment supports compliance with HIPAA, GDPR, and PIPEDA while remaining scalable for future growth.

### Recommendations for Future Improvement

1. **Automation with Infrastructure-as-Code:**  
   Implement Bicep, Terraform, or Azure Blueprints to automate landing zone deployment and ensure consistent governance across all environments.

2. **Enhanced Resilience and Multi-Region Design:**  
   Extend disaster recovery to additional Azure regions or incorporate multi-cloud strategies to improve high availability for critical healthcare systems.

## 7. **Conceptual Zero Trust Landing Zone Diagram**

Below is a **Mermaid diagram**:

```mermaid
flowchart TD

    subgraph MG["Management Groups"]
        R["Root"]
        C["CloudMed"]
        P["Platform"]
        PR["Production"]
        D["Development"]
    end

    R --> C
    C --> P
    C --> PR
    C --> D

    subgraph Hub["Hub Network"]
        FW["Azure Firewall"]
        BAS["Azure Bastion"]
        DNS["Private DNS"]
        LOG["Log Analytics"]
    end

    subgraph Spokes["Workload Spokes"]
        APP["App Tier VNet"]
        API["API Tier VNet"]
        DB["Data Tier VNet\n(Private Endpoints)"]
    end

    FW --> APP
    FW --> API
    FW --> DB
    BAS --> APP
    LOG --> APP
    LOG --> API
    LOG --> DB




