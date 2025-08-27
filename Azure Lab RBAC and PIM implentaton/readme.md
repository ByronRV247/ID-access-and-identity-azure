# 🔐 Azure Privileged Identity Management (PIM) Lab

This repository contains a hands-on lab to configure and test **Azure AD Privileged Identity Management (PIM)** using **role-assignable groups**.  
The goal is to practice **just-in-time (JIT)** privileged access, approval workflows, and security best practices in Azure Active Directory.

---

## 🎯 Objectives
- Enable **PIM** in Azure Active Directory.
- Assign **Azure AD roles** to role-assignable groups.
- Configure **eligibility vs. active assignments**.
- Apply **activation settings** (MFA, justification, approval).
- Test JIT role activation with demo users.

---

## 📂 Groups in the Lab

| Group Name        | Object ID                              | Type             | Role Assignment Example        |
|-------------------|----------------------------------------|------------------|--------------------------------|
| **Sales**         | 21ce7e3b-15f7-4fe7-9adf-9eb215a91382   | Standard Group   | None (non-privileged)          |
| **HRRoleGroup**   | 2864e2d8-403c-4257-af4f-b171365fc269   | Role-Assignable  | User Administrator             |
| **AdminRoleGroup**| 6b1f74b5-0037-4ac7-9aa7-0ad1d7303550   | Role-Assignable  | Global Administrator           |
| **HelpDeskRoleGroup** | f256e0e0-8749-4dc8-ad4f-dc04c46b5c5f | Role-Assignable  | Helpdesk Administrator         |

---

## ⚙️ Steps to Reproduce

### 1. Enable PIM
1. Log into [Azure Portal](https://portal.azure.com/).
2. Navigate to **Azure AD → Privileged Identity Management**.
3. Consent to enable PIM in the tenant.

---

### 2. Assign Roles to Groups
Use Microsoft Graph PowerShell:

```powershell
# Assign Global Administrator to AdminRoleGroup
$role = Get-MgDirectoryRole | Where-Object {$_.DisplayName -eq "Global Administrator"}
New-MgDirectoryRoleMemberByRef -DirectoryRoleId $role.Id -OdataId "https://graph.microsoft.com/v1.0/groups/6b1f74b5-0037-4ac7-9aa7-0ad1d7303550"

# Assign Helpdesk Administrator to HelpDeskRoleGroup
$role = Get-MgDirectoryRole | Where-Object {$_.DisplayName -eq "Helpdesk Administrator"}
New-MgDirectoryRoleMemberByRef -DirectoryRoleId $role.Id -OdataId "https://graph.microsoft.com/v1.0/groups/f256e0e0-8749-4dc8-ad4f-dc04c46b5c5f"

# Assign User Administrator to HRRoleGroup
$role = Get-MgDirectoryRole | Where-Object {$_.DisplayName -eq "User Administrator"}
New-MgDirectoryRoleMemberByRef -DirectoryRoleId $role.Id -OdataId "https://graph.microsoft.com/v1.0/groups/2864e2d8-403c-4257-af4f-b171365fc269"
