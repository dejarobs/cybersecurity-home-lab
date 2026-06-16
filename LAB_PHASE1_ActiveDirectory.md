# Home Cybersecurity Lab — Phase 1: Active Directory Environment Setup

**Author:** Deja Roberts  
**Date:** [MM/DD/YYYY]  
**Platform:** UTM on macOS (Apple Silicon M-series)  
**Status:** [ ] In Progress / [ ] Complete

---

## Objective

Build a functional Active Directory (AD) domain environment using Windows Server 2022 as the domain controller and a Windows 10/11 client machine joined to the domain. This phase establishes the identity and access management (IAM) foundation for all subsequent lab phases, including Splunk log ingestion and simulated attack detection.

---

## Environment

| Component | Details |
|---|---|
| Host Machine | MacBook Air M-series, 16GB RAM, 256GB storage |
| Virtualization | UTM |
| Guest OS 1 | Windows Server 2022 (Domain Controller) |
| Guest OS 2 | Windows 10 or 11 (Domain Client) |
| Network Config | Internal network (host-only, isolated) |
| Tools Used | Active Directory Domain Services (AD DS), DNS, Group Policy |

---

## Steps Taken

### Step 1: Install Windows Server 2022 in UTM
- Download Windows Server 2022 evaluation ISO from Microsoft
- Create a new VM in UTM: ARM64 architecture, 4GB RAM minimum, 60GB virtual disk
- Complete installation — select "Desktop Experience" for GUI
- Set a strong Administrator password

> 📸 *Screenshot: UTM VM settings showing resource allocation*

---

### Step 2: Configure Static IP and Rename the Server
- Set a static IP address (e.g., 192.168.1.10) via Network Adapter settings
- Rename the server (e.g., DC01) before promoting to domain controller
- Restart to apply changes

> 📸 *Screenshot: Network adapter IP configuration*

---

### Step 3: Install Active Directory Domain Services (AD DS)
- Open Server Manager → Add Roles and Features
- Select Active Directory Domain Services
- Complete the wizard and install

> 📸 *Screenshot: Server Manager showing AD DS role installed*

---

### Step 4: Promote Server to Domain Controller
- In Server Manager, click the notification flag → Promote this server to a domain controller
- Select "Add a new forest" — set a root domain name (e.g., lab.local)
- Set Directory Services Restore Mode (DSRM) password
- Complete promotion and allow server to restart

> 📸 *Screenshot: Domain controller promotion wizard — forest/domain name screen*

---

### Step 5: Create Organizational Units (OUs), Users, and Groups
- Open Active Directory Users and Computers (ADUC)
- Create OUs: e.g., IT, Finance, HR
- Create at least 3 standard user accounts and 1 admin account
- Assign users to groups

> 📸 *Screenshot: ADUC showing OUs and user accounts*

---

### Step 6: Join Windows Client to the Domain
- Configure the client VM's DNS to point to the DC's static IP
- Navigate to System Properties → Change domain → enter lab.local
- Authenticate with domain admin credentials
- Restart and log in as a domain user

> 📸 *Screenshot: Client machine successfully joined to lab.local*

---

### Step 7: Configure a Basic Group Policy Object (GPO)
- Open Group Policy Management on the DC
- Create a new GPO (e.g., Password Policy, Account Lockout Policy)
- Link to the domain or a specific OU
- Run `gpupdate /force` on the client to apply

> 📸 *Screenshot: GPO editor showing policy settings*

---

## Findings / Observations

> Fill this in after completing the phase.

- **Finding 1:** [e.g., Domain join succeeded; client now authenticates against DC01]
- **Finding 2:** [e.g., GPO applied correctly — confirmed via `gpresult /r` on client]
- **Finding 3:** [e.g., Event ID 4720 logged in Security event log when new user account was created]

---

## Framework Mapping

| Action Performed | Framework Reference |
|---|---|
| Created user accounts and groups with least privilege | NIST SP 800-53: AC-2 – Account Management |
| Configured password and lockout policy via GPO | NIST SP 800-53: IA-5 – Authenticator Management |
| Reviewed Security event logs for account activity | NIST SP 800-137: Continuous Monitoring |
| Documented identity structure (OUs, roles, groups) | NIST SP 800-37: RMF Step 1 – Categorize (system inventory) |

---

## Lessons Learned

> Complete after finishing the phase.

1. 
2. 
3. 

---

## Real-World Relevance

Active Directory is the identity backbone of most enterprise Windows environments. This phase mirrors the IAM infrastructure a Systems Administrator or IAM Analyst would manage day-to-day — provisioning accounts, enforcing access policies, and maintaining an auditable user directory. It also reflects the access control review processes required under NIST SP 800-53 AC controls, directly relevant to GRC and RMF roles.

---

## Next Phase Preview

Phase 2 will install Splunk on a dedicated VM and configure Windows Event Log forwarding from the domain controller and client, enabling centralized log collection and alert creation.

---

*Lab series: [Link to repo README or index]*
