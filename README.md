# Active Directory
Active Directory: How to add users, groups and group policies using the graphical interface (PowerShell is only used for the installation and the configuration of the AC)

Introduction
This guide documents the process of setting up and configuring Active Directory in a Windows Server environment. It serves as a step-by-step reference for installing Active Directory Domain Services (AD DS), managing users and groups, and configuring group policies.

Prerequisites

Windows Server (any recent version)
Administrator access
PowerShell access

Installation Process
1. Installing Active Directory Domain Services
Using PowerShell (Automated Method):
powershellCopy# Run PowerShell as Administrator
C:\Qwiklabs\ADSetup\active_directory_install.ps1

Note: After installation, the server will automatically restart

Post-Restart Configuration:
powershellCopy# Run after server restart
C:\Qwiklabs\ADSetup\configure_active_directory.ps1
2. User Management Guide
Creating a New User

Open Active Directory Administrative Center (ADAC)

Search for "Active" in Windows Start menu
Select "Active Directory Administrative Center"


Navigate to User Creation

Click on your domain (example.com)
Double-click "Users" container
In the Tasks pane, click "New" → "User"


Configure New User Settings
CopyRequired Fields:
- First name
- Last name
- User UPN logon
- Password

Enable the Account

Right-click on the disabled user
Select "Enable"
If error occurs, set a password first:

Right-click user → "Reset password"
Enter new password
Check "User must change password at next logon"
Click "OK"





3. Group Management Guide
Creating a New Group

In ADAC:

Navigate to Users container
Tasks pane → "New" → "Group"


Configure Group Settings
CopyRequired Fields:
- Group name (e.g., "Python Developers")
- Group scope (Usually "Global")
- Group type (Usually "Security")


Adding Group to Another Group
Method 1: Via Group Properties

Double-click target group
Click "Members"
Click "Add"
Enter group name
Click "Check Names" to verify
Click "OK"

Method 2: Via Context Menu

Right-click group
Select "Add to another group"
Enter parent group name
Click "Check Names"
Click "OK"

4. Group Policy Configuration
Creating and Configuring a GPO

Open Group Policy Management

Search for "Group Policy Management" in Start menu


Create New GPO

Navigate to domain → desired OU
Right-click → "Create a GPO in this domain and Link it here"
Enter name (e.g., "New Wallpaper")


Edit GPO

Right-click new GPO → "Edit"
Navigate policy tree:
CopyUser Configuration →
Policies →
Administrative Templates →
Desktop →
Desktop



Configure Policy Settings
Example - Setting Wallpaper:

Double-click "Desktop Wallpaper"
Select "Enabled"
Enter wallpaper path (e.g., C:\Qwiklabs\wallpaper.jpg)
Click "OK"


Verify Policy Settings

Return to Group Policy Management
Select your GPO
View "Settings" tab



Common Tasks Quick Reference
Modifying Group Membership
CopyTo Add User to Group:
1. Double-click group
2. Click "Members" → "Add"
3. Enter username
4. Click "Check Names" → "OK"

To Remove User from Group:
1. Double-click group
2. Select user in Members list
3. Click "Remove"
4. Click "OK"
Checking Group Membership
CopyTo Check User's Groups:
1. Double-click user
2. Click "Member Of" tab
Troubleshooting
Common Issues and Solutions

Unable to Enable User

Solution: Ensure password meets complexity requirements


Group Policy Not Applying

Run gpupdate /force in Command Prompt
Check GPO link status
Verify user/computer is in correct OU



Verification Commands
powershellCopy# Force Group Policy Update
gpupdate /force

# Check Group Policy Results
gpresult /r

# Check Active Directory Replication
repadmin /replsummary
Best Practices

Always use strong passwords
Follow the principle of least privilege
Document all policy changes
Test GPOs before broad deployment
Regularly review user and group memberships

