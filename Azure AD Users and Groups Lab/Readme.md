Lab Objective

The goal of this lab was to practice Azure Active Directory (Azure AD) user and group management by:

Creating users in Azure AD.

Creating security groups to represent departments and roles.

Automatically assigning users to the correct groups based on their JobTitle.

Verifying that group memberships are correct.

Steps Performed
1. Created Users

Added multiple users with realistic JobTitles, including:

Sales: Alice, Bob Patel, Test User 01

HR: Charlie Kim, Hana Suzuki, Ivan Petrovski

Helpdesk: Diana Lopez, Ethan Wright, Fatima Hassan, Julia Martínez

Break-Glass account: Emergency-Admin

2. Created Security Groups

Created the following groups to match department roles:

Lab-HR

Lab-Sales

Lab-Helpdesk

Break-glass

3. Assigned Users to Groups

Created a PowerShell script using Microsoft Graph module to automatically assign users to the correct group based on JobTitle.

Handled typos and missing JobTitles by skipping users without a proper mapping.

Verified assignments using Get-MgGroupMember and cross-checking user JobTitles.

4. Verification

Confirmed that each user was a member of their respective group.

Used scripts to list all groups and members with DisplayName, UserPrincipalName, and JobTitle.

PowerShell Scripts Used

User creation – New-MgUser for adding users.

Group creation – New-MgGroup for creating security groups.

Automated assignment – looping through users and mapping JobTitles to groups.

Verification – listing all groups and members to confirm assignments.

Conclusion

This lab provided hands-on experience in Azure AD user and group management, including:

Automating user-to-group assignments using PowerShell and Microsoft Graph.

Handling different JobTitles and edge cases in a real-world scenario.

Verifying group memberships and ensuring accurate role-based access.

This exercise is a fundamental step toward understanding identity and access management in the cloud, which is essential for entry-level IT and cloud security roles.
