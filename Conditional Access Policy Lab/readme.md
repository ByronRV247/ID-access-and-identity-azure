# Conditional Access Policies – Microsoft Entra ID

This repository documents the setup of **three Conditional Access (CA) policies** in Microsoft Entra ID (Azure AD) to strengthen identity and access security.

## 🚀 Overview
The following Conditional Access policies were implemented and tested:

1. **Require MFA for All Users**  
   Ensures that all sign-ins require Multi-Factor Authentication (MFA).

2. **Block Legacy Authentication**  
   Blocks sign-ins using legacy authentication protocols (e.g., POP, IMAP, SMTP) which do not support modern security methods.

3. **Block Access Outside Costa Rica**  
   Restricts access to Microsoft cloud apps, blocking sign-ins from any location outside Costa Rica.

---

## 📋 Requirements
- **Microsoft Entra ID Premium P1** (included in Microsoft 365 E3/E5, or Business Premium).  
- Global Administrator or Conditional Access Administrator permissions.  
- At least one **break-glass emergency account** excluded from CA policies.  
- [Exchange Online Management PowerShell module](https://learn.microsoft.com/powershell/exchange/exchange-online-powershell-v2).

---

## ⚙️ Policy Setup

### 1. Require MFA for All Users
- **Assignments**  
  - Users/Groups → All users (exclude emergency admin).  
  - Cloud apps → All apps.  
- **Access controls**  
  - Grant → Require Multi-Factor Authentication.  
- **Enable policy** → On.

---

### 2. Block Legacy Authentication
- **Assignments**  
  - Users/Groups → All users (exclude emergency admin).  
  - Cloud apps → All apps.  
- **Conditions**  
  - Client apps → Include “Other clients” (legacy auth).  
- **Access controls**  
  - Block access.  
- **Enable policy** → On.

---

### 3. Block Access Outside Costa Rica
- **Named Location**  
  - Created `Costa Rica - Country` (country/region = Costa Rica).  
- **Assignments**  
  - Users/Groups → IT group (exclude emergency admin).  
  - Cloud apps → All apps.  
- **Conditions**  
  - Locations → Include *Any location*, Exclude *Costa Rica - Country*.  
- **Access controls**  
  - Block access.  
- **Enable policy** → On.

---

## 🔍 Testing

### Tools
- **What If** tool → Simulate policy effect on test users.  
- **Sign-in Logs** → Review actual policy application per login.  

### Test Scenarios
1. **Require MFA**  
   - Sign in with test account → prompted for MFA.  

2. **Block Legacy Authentication**  
   - Attempt login via Outlook 2010/POP/IMAP → blocked.  

3. **Block Access Outside Costa Rica**  
   - Sign in from Costa Rica IP → allowed.  
   - Sign in using VPN with foreign IP → blocked.  

---

## 🛡️ Best Practices
- Always **exclude at least one emergency admin** from Conditional Access.  
- Start new policies in **Report-only mode** before enforcing.  
- Regularly monitor **Sign-in Logs** for policy impact and possible false positives.  
- Document rollback steps (how to disable a policy if lockout occurs).  

---

## 📚 References
- [Microsoft Learn – Conditional Access Overview](https://learn.microsoft.com/entra/identity/conditional-access/overview)  
- [Named Locations in Conditional Access](https://learn.microsoft.com/entra/identity/conditional-access/location-condition)  
- [Report-only Mode](https://learn.microsoft.com/entra/identity/conditional-access/concept-conditional-access-report-only)  
