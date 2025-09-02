# Salesforce + Azure AD SAML Lab

## Overview
This lab demonstrates how to configure **SAML 2.0 Single Sign-On (SSO)** between **Salesforce** and **Azure Active Directory**. After completion, users can log in to Salesforce via Azure AD without entering separate credentials.

## Prerequisites
- Salesforce admin access
- Azure AD tenant and admin access
- Base64 certificate from Azure AD

## Steps

### 1. Configure SAML in Salesforce
1. Setup → Single Sign-On Settings → New
2. Enter:
   - Name: `Azure AD SSO`
   - API Name: `Azure_AD_SSO`
   - Version: `2.0`
   - Entity ID / Issuer: `https://inspiration-site-5524.my.salesforce.com`
   - Identity Provider Certificate: Upload `.cer` from Azure AD
   - Signature Method: `RSA-SHA256`
   - Name ID Format: `Username (Email)`
   - Identity Location: `Subject`
   - SP-initiated: `HTTP POST`
3. Save and note ACS URL and Logout URL.

### 2. Configure Azure AD SAML
1. Azure AD → Enterprise Applications → Salesforce → SAML
2. Enter:
   - Identifier (Entity ID): `https://inspiration-site-5524.my.salesforce.com`
   - Reply URL (ACS URL): `https://inspiration-site-5524.my.salesforce.com/services/auth/sp/saml2/acs`
   - Sign-on URL: `https://inspiration-site-5524.my.salesforce.com`
   - Logout URL: `https://inspiration-site-5524.my.salesforce.com/services/auth/sp/saml2/logout`
   - NameID: `user.userprincipalname`
3. Assign users.

### 3. Map Users
- Federation ID in Salesforce = UPN/email in Azure AD

### 4. Test
- Use Azure AD Test SSO or MyApps portal to verify login.

## Notes
- Entity ID is your Salesforce org URL.
- ACS URL is where Salesforce receives SAML assertions.
- Base64 certificate is required from Azure AD.
- Relay State is optional.

