# 🖥 Active Directory Infrastructure Lab

**Windows Server 2022 + Windows 10 Pro**

![Infrastructure Design](/images/01-infra-design-diagram.png)

---

## 📌 Project Overview

This project simulates the deployment of a centralized **Active Directory environment** for a small business scenario. The lab demonstrates:

- Domain services configuration  
- Organizational structure design  
- Group Policy enforcement  
- Secure file sharing using Windows Server 2022 and Windows 10 Pro in a virtualized environment  

---

## 🏢 Business Scenario

A fictional company, **TechSolutions Ltd**, requires:

- Centralized domain authentication  
- Department-based user organization (**HR & IT**)  
- Password security enforcement  
- Account lockout protection  
- Department-level shared folder access control  
- Restricted system settings for HR users  
- Scalable onboarding process  

---

## 🖥 Infrastructure

| **Component**       | **Name**                 | **Role**                               |
|--------------------|--------------------------|----------------------------------------|
| Domain Controller   | DC-01                    | AD DS + DNS + DHCP + File Server       |
| Client Machine      | WS-01                    | Domain-joined workstation              |
| Domain Name         | corp.techsolutions.local | Internal Active Directory Domain       |
| Network             | 192.168.56.0/24          | VirtualBox NAT Network                 |


---

## 🔧 Implementation Summary

### 1️⃣ Server Configuration

- Configured static IP: `192.168.56.10`  
- Configured DNS pointing to Domain Controller  
- Installed **Active Directory Domain Services (AD DS)**  
- Promoted server to **Domain Controller**  
- Created new forest: `corp.techsolutions.local`  
- Configured DHCP scope: `192.168.56.20 – 192.168.56.100`  

 ![AD DS Forest Deployment](/images/02-add-ad-ds-forest-deployment-winserver.png)

---

### 2️⃣ Organizational Structure

- Created **Organizational Units (OUs)**:  
  - HR  
  - IT  
  - Workstations  

- Created **Security Groups**:  
  - HR_Users  
  - IT_Users  

- Assigned users based on department  
- Implemented **group-based permission model** (no direct user permissions)  

 ![OU & Users](/images/04-new-user-added-to-hr-ou-winserver.png)

---

### 3️⃣ Client Deployment / Domain Join

- Configured Windows 10 client DNS  
- Joined client to domain  
- Verified authentication with domain credentials  
- Confirmed DHCP IP assignment  

 ![Domain Joined Client](/images/03-domain-joined-win10-shown-onserver-winserver.png)

---

### 4️⃣ Group Policy Implementation

**Domain-Level Policies**:

- Minimum password length: 8 characters  
- Account lockout threshold: 3 failed attempts  

 ![Account Lockout Policy](/images/06-account-lockout-3invalid-pass-config-winserver.png)

**HR Security Restrictions**:

- Restricted Control Panel access  
- Applied using **Security Filtering** (`HR_Users` group)  
- Linked at domain level for scalable management  

 ![Minimum Password Length](/images/05-hr-user-sara-control-panel-unaccesible-win10-error.png)  


---

### 5️⃣ File Server & NTFS Permissions

- Created shared folders: `HRFiles`, `ITFiles`  
- Configured **NTFS & Share permissions** using Security Groups    

 ![IT Folder Permissions](/images/08-folder-sharing-config-for-it-users-ITFiles-folder-winser.png)

---

### 6️⃣ Drive Mapping & Automation

- Configured automatic drive mapping based on group membership  

**Logic:**  
- User in HR OU + Member of HR_Users → HR drive mapped  

- Ensured **scalable onboarding** without manual configuration  

- Prevented cross-department access  
- Followed **least privilege principle**

 ![HR Access Denied IT Folder](/images/09-hr-cant-access-it-folder-win10.png)

---

### 7️⃣ Validation / Testing

| **Test Scenario**         | **Expected Result**                     | **Status**        |
|----------------------------|----------------------------------------|-----------------|
| 3 Invalid Logins           | Account Lockout                        | ✅ Successful    |
| HR Access IT Folder        | Access Denied                           | ✅ Successful    |
| IT Access HR Folder        | Access Denied                           | ✅ Successful    |
| HR Control Panel Access    | Blocked                                 | ✅ Successful    |
| New HR User Creation       | Automatic Policies & Drive Mapping     | ✅ Successful    |

 ![User Locked After 3 Invalid Attempts](/images/07-user-locked-invalid-password-3--wind10.png)  

---

## 🔍 Skills Demonstrated

- Active Directory Domain Services (AD DS)  
- DNS & DHCP Configuration  
- OU & Security Group Design  
- Group Policy Management  
- NTFS Permissions & Access Control  
- Domain Join & Client Management  
- Scalable Access Control Design  
- Security Filtering in GPO  

---

## ✅ Conclusion

This lab demonstrates practical implementation of a **structured Active Directory environment** with:

- Centralized authentication  
- Enforced security policies  
- Scalable department-based access control  

The project reflects foundational skills relevant to **entry-level IT Support** and **Junior System Administrator** roles.

⭐ If you found this project helpful, consider giving it a star!
