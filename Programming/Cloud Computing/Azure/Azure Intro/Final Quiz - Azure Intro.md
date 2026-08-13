# Azure Questions and Answers

---

### 1. Which of the following pricing options will let you use your existing Windows license with Azure VMs?
**Answer:** Hybrid Benefit  
**Explanation:** The Azure Hybrid Benefit allows you to use your existing on-premises Windows Server or SQL Server licenses with Software Assurance to save costs when running Azure Virtual Machines.

---

### 2. Which of the following resources is optional at the time of creation for a VM in Azure?  
**Answer:** Public IP  
**Explanation:** A VM can be created without a public IP if it only needs private/internal access. Resource groups, VNets, and NICs are required.

---

### 3. How many fault domains and update domains are assigned to an Availability Set by default?  
**Answer:** 2 and 5 respectively  
**Explanation:** Default Fault Domains (FD) = 2, Update Domains (UD) = 5.

---

### 4. At which point in a VM's life cycle can it be assigned to an availability set?  
**Answer:** At time of creation  
**Explanation:** A VM cannot be added to an Availability Set after deployment; it must be assigned during creation.

---

### 5. Which layer of the OSI stack does the Azure Load Balancer operate in?  
**Answer:** Layer 4  
**Explanation:** Azure Load Balancer operates at the Transport layer (Layer 4), routing traffic based on IP and TCP/UDP ports.

---

### 6. Which of the following would qualify as a point-to-site VPN connection?  
**Answer:** Local machine to VPN gateway  
**Explanation:** P2S VPN connects a single client device directly to an Azure VNet via a VPN gateway.

---

### 7. Which Azure storage replication option will allow you to read from the secondary copy even if the primary region isn’t down?  
**Answer:** RA-GRS  
**Explanation:** Read-Access Geo-Redundant Storage allows read access to the secondary region even when the primary is healthy.

---

### 8. How many data centers are used when a storage replica is configured using Geo-zone redundant storage?  
**Answer:** 4  
**Explanation:** GZRS replicates across 3 availability zones in the primary region plus 1 datacenter in the secondary region = 4 datacenters.

---

### 9. Which of the following is true for VMs deployed in an Availability Set?  
**Answer:** Apps can be installed using extensions  
**Explanation:** VM extensions allow automated software installation and configuration.

---

### 10. What is the primary difference between LRS and ZRS?  
**Answer:** LRS uses 1 data center while ZRS uses 3  
**Explanation:** LRS replicates within a single datacenter; ZRS replicates across 3 availability zones in the same region.

---

### 11. At which level are lifecycle management rules for Blob storage applied?  
**Answer:** Storage account level  
**Explanation:** Rules apply at the storage account or container level, not individual files/blobs.

---

### 12. Which property allows a VNet to use a VPN Gateway connected to a peered VNet?  
**Answer:** Gateway transit  
**Explanation:** Gateway transit allows a peered VNet to use the primary VNet's VPN Gateway.

---

### 13. Which timer code is used to schedule an Azure Function to run every 24 hours?  
**Answer:** 0 0 */24 * * *  
**Explanation:** CRON expression specifies 0 seconds, 0 minutes, every 24 hours.

---

### 14. Which of the following is true of internal load balancers?  
**Answer:** They are deployed in a virtual network  
**Explanation:** Internal Load Balancers are private to a VNet and do not have a public IP.

---

### 15. Select the correct order of Azure hierarchy:  
**Answer:** resources < resource groups < subscriptions < management group  
**Explanation:** Smallest to largest: Resources → Resource Groups → Subscriptions → Management Groups.

---

### 16. In Azure, Network Security Group rules are evaluated in order of:  
**Answer:** Priority  
**Explanation:** Rules are evaluated by ascending priority; first match applies.

---

### 17. Which VM properties may change depending on VM size?  
**Answer:** All of these  
**Explanation:** vCPUs, memory, and max number of disks all depend on VM size.

---

### 18. Which of the following qualifies as a destination for inbound NSG rules?  
**Answer:** NIC  
**Explanation:** NSG rules are applied to NICs or subnets, not VMs or resource groups directly.

---

### 19. Which of the following is NOT a feature of Azure AD?  
**Answer:** Virtual machines VMs management  
**Explanation:** Azure AD provides identity and access management, not VM management.

---

### 20. Which Azure AD service allows users to reset passwords without administrator intervention?  
**Answer:** Self-Service Password Reset (SSPR)  
**Explanation:** Users can reset or unlock their own passwords without IT helpdesk.

---

### 21. What is a key benefit of using Managed Identities?  
**Answer:** Securely accessing Azure services without managing credentials  
**Explanation:** Managed Identities eliminate the need to store secrets/credentials in applications.

---

### 22. What is the main purpose of Azure Key Vault?  
**Answer:** To secure and manage secrets, encryption keys, and certificates  
**Explanation:** Protects sensitive information and controls access.

---

### 23. Which of the following is NOT a feature of Azure AD?  
**Answer:** Virtual machines (VMs) management  
**Explanation:** VM management is handled by Azure Resource Manager, not Azure AD.

---

### 24. What is the main advantage of using Managed Identities in Azure?  
**Answer:** Eliminating the need to store credentials in application code for accessing Azure resources  
**Explanation:** Azure handles authentication and credential rotation automatically.

---

### 25. In Azure AD, what is CSPM and CWPP?  

**Answer:**  

- **CSPM (Cloud Security Posture Management):** Continuously monitors cloud resources for misconfigurations and compliance gaps.  
- **CWPP (Cloud Workload Protection Platform):** Provides runtime protection for workloads like VMs, containers, and serverless functions.  

| Feature | CSPM | CWPP |
|---------|------|------|
| Focus | Configuration & compliance | Runtime protection |
| Scope | Cloud resources | Workloads (VMs, containers, serverless) |
| Goal | Prevent misconfigurations | Prevent attacks/exploits |

