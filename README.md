<p align="center">
<img src="https://github.com/user-attachments/assets/d611513a-0ed2-4ce1-9ad1-312f29b3be26" height="250" width="400" />
</p>

<h1>Group Policy Object Configuration</h1>
This tutorial outlines the implementation of Group Policy Objects within Microsoft Azure VMs.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Group Policy Management Console
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>Group Policy Overview</h2>

Group Policy (GP) is a neccesary part of Active Directory. It allows system admins to configure user and domain properties on a wide scale. Since GP has hundreds, if not thousands of policies to configure, this will just be a mini lesson on how to use it. 

Here we will be configuring our accont lockout threshhold properties, which in lamens terms is just a policy that determines how many attempts a user gets to log into their account before being locked out, for how long theyre locked out for and even how long it takes for the failed attempts counter to reset. While this is only a dot in the vast amount of things we can do with GP, all other group policies follow the same format of looking for them and configuring them.

<h2>Configuration Steps</h2>
Configuring any group policy follows the same process:
- Opening the Group Policy Management Console (GPMC)
- Creating a Group Policy Object (GPO)
- Locating the Policy
- Configuring the Policy
- Linking the GPO to an OU
- Updating the group policy

<h2>Deployment and Configuration</h2>

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
  texttexttext
</p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
