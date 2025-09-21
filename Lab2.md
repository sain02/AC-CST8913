# Lab 2 – Cloud Deployment Models: IaaS vs PaaS

**Name:** Saizal Saini 

**Student No:** 041168394 

**Course:** Cloud Migration

---

## Scenario
The application under consideration consists of:
- **Frontend (UI):** React
- **Backend (Web Server):** Flask
- **Database Layer:** PostgreSQL

The goal of this lab is to analyze how the application can be deployed in the cloud using **IaaS (Infrastructure as a Service)** and **PaaS (Platform as a Service)** models. Each deployment model has its own architecture, trade-offs, and cloud services.

---

## I. Deployment Using IaaS

### Architecture Diagram
![IaaS Architecture](Screenshot%202025-09-19%20205322.png)

### Explanation
In an **IaaS deployment**, the cloud provider supplies the fundamental compute, storage, and networking infrastructure. The application team is responsible for installing, configuring, and maintaining the operating system, runtime, middleware, and application stack.

1. **User Browser**  
   - End users access the application through a web browser.

2. **Load Balancer**  
   - Distributes incoming traffic across multiple virtual machines (VMs).
   - Improves scalability and availability.

3. **Virtual Machines**  
   - **VM: React UI** – Hosts the frontend React application, served by a web server like Nginx or Apache.  
   - **VM: Flask Server** – Hosts the Flask backend API, running on Python.  
   - **VM: PostgreSQL Database** – Dedicated VM for running the PostgreSQL database.  

### Characteristics of IaaS
- Provides maximum control over the environment (OS, libraries, configurations).  
- Requires manual management of patching, scaling, and updates.  
- Flexibility for custom deployments, but higher operational overhead.  
- Example services: AWS EC2 + ELB, Azure Virtual Machines + Load Balancer, GCP Compute Engine.  

---

## II. Deployment Using PaaS

### Architecture Diagram
![PaaS Architecture](Screenshot%202025-09-19%20210001.png)

### Explanation
In a **PaaS deployment**, the cloud provider manages much of the application stack, including runtime, middleware, scalability, and database services. The development team focuses mainly on writing and deploying application code.

1. **User Browser**  
   - End users connect to the application via the internet.

2. **Managed Load Balancer**  
   - Automatically distributes requests across backend services.  
   - Provided and maintained by the cloud provider.  

3. **React Frontend**  
   - Deployed on cloud storage (e.g., AWS S3, Azure Blob Storage, GCP Cloud Storage).  
   - Served globally via a Content Delivery Network (CDN) for faster performance.  

4. **Flask Backend**  
   - Deployed on a managed service such as:  
     - AWS Elastic Beanstalk  
     - Azure App Service  
     - Google Cloud Run / App Engine  
   - Automatically handles scaling, runtime management, and updates.  

5. **Managed PostgreSQL Database**  
   - Hosted on a fully managed service (e.g., AWS RDS, Azure Database for PostgreSQL, GCP Cloud SQL).  
   - Cloud provider handles backups, patching, scaling, and monitoring.  

### Characteristics of PaaS
- Reduces operational overhead since infrastructure and runtime are managed.  
- Offers built-in scalability and availability.  
- Limited flexibility compared to IaaS (restricted OS and configuration options).  
- Example services: AWS Elastic Beanstalk + RDS, Azure App Service + Azure Database for PostgreSQL, GCP Cloud Run + Cloud SQL.  

---

## III. Comparison of IaaS vs. PaaS

| Aspect             | IaaS Deployment                                | PaaS Deployment                              |
|--------------------|-----------------------------------------------|----------------------------------------------|
| **Control**        | Full control over OS, runtime, middleware     | Limited control; provider manages environment |
| **Management**     | Manual setup, scaling, patching, monitoring   | Automated scaling, patching, monitoring      |
| **Flexibility**    | High flexibility (custom installs/configs)    | Restricted to supported runtimes/services     |
| **Complexity**     | High – requires DevOps/infra expertise        | Lower – focus on app code                    |
| **Use Case**       | Best for legacy apps, custom configs, strict compliance | Best for rapid development, scaling, modern apps |

---

## Conclusion
- **IaaS** is ideal when you need complete control and customization but are willing to manage infrastructure overhead.  
- **PaaS** is ideal when speed, scalability, and reduced maintenance are the priority, allowing teams to focus on development rather than infrastructure management.  

---
# THANKS