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

Group Policies (GP) are a neccesary part of system administration. It allows system admins to configure user and domain properties on a wide scale. Since GP has hundreds, if not thousands of policies to configure, this will just be a mini lesson on how to use it. 

This tutorial will be on configuring our account lockout threshold properties, which in lamens terms is a set of policies that determine how many attempts a user gets to log into their account before being locked out, for how long theyre locked out for and even how long it takes for the failed attempts counter to reset. While this is only a dot in the vast amount of things we can do with GP, all other group policies follow the same format when we configure them.

<h2>Configuration Process</h2>
Configuring any group policy follows the same process:

- Opening the Group Policy Management Console (GPMC)
- Creating a Group Policy Object (GPO)
- Locating the Policy
- Configuring the Policy
- Linking the GPO to an OU
- Updating the group policy

<h2>Deployment and Configuration</h2>

<ins>**Open the Group Policy Management Console**<ins/>

You can open the group GPMC by searching for the group policy management app within your domain contoller.

The app appears on the left while the right window is what it looks like when its open.


<img src="https://github.com/user-attachments/assets/8d83a63b-31ce-436c-938c-e3cca512835f" height="300" width="700">


<ins>**Create a Group Policy Object**<ins/>

We can create a new group policy object by using the following path:

GPMC > Forest:*your domain* > Domains > Your Domain > Group Policy Objects > Right Click + New > *Create a Name* 

In this instance we will call our new group policy "Account Lockout Policy"

<img src="https://github.com/user-attachments/assets/5f73ceda-8264-4a4c-8bd5-38662578ac21" height="400" width="750">

<ins>**Locating Our Policy**<ins/>

The GPMC has a plethora of things we can do to configure our policies for people within our domain. Each policy has its own unique path to follow for its configuration. Here is the path that we will be taking to get to the account lockout policy from our newly created GPO:

Account Lockout Policy > Computer Configuration > Policies > Windows Settings > Security Settings > Account Policies > Account Lockout Policy.


<img src="https://github.com/user-attachments/assets/a37aba43-7d2d-4cf3-88a2-d59fb950cad7" height="400" width="750">


<ins>**Configuring the Group Policy**<ins/>

Now that weve arrived at the account lockout policy for our domain, we need to configure it. We can configure the following settings to the standards of whatever our organization deems necessary. For our case, we will be configuring our account lockout policy with a 30 minute lockout duration, 3 invalid attempts for lockout, and have our account lockout counter reset after 15 minutes. 

**Account Lockout Duration** - The time in minutes that an account remains locked before it is automatically unlocked.
- Configuration: Double-click on this setting, select Define this policy setting, and then set the duration (30 minutes).


**Account Lockout Threshold** - The number of failed logon attempts that will trigger an account lockout.
- Configuration: Double-click on this setting, select Define this policy setting, and then set the threshold (3 invalid attempts).


**Reset Account Lockout Counter After** - The time in minutes after which the failed logon attempts counter is reset to 0, assuming there are no additional failed logon attempts.
- Configuration: Double-click on this setting, select Define this policy setting, and then set the time (15 minutes).

**Allow Administrator Account Lockout** - Whether or not accounts with the administrator tag are able to be locked out of. It's reccomended to have this setting enabled in case someone tries to login to an administrator account, which if put in the wrong hands, can cause severe damage to the domain.
- Configuration: Double-click on this setting, select Define this policy setting, and then set it as enabled/disabled.

Once you have configured these settings, your account lockout policy page should look like this:

<img src=https://github.com/user-attachments/assets/7aa30408-1ae8-4ac0-b525-927f34baa76f >




**If you are ever not sure as to what a certain group policy configuration does, they each have an explination tab within their configuration which gives a thourough explaination on what it does, and how it works.**

<img src="https://github.com/user-attachments/assets/76a8ad88-fe5b-451a-80d4-c1e0e20b5f2a" height="500" width="300"> <img src="https://github.com/user-attachments/assets/4a8b72d7-db86-4ea3-902b-6273e7fb3d5f" height="500" width="300"> <img src="https://github.com/user-attachments/assets/33d958b6-c78f-4e17-8c95-f9f85e08b11f" height="500" width="300">

**IMPORTANT CONSIDERATIONS**

Account Lockout Threshold: Setting this too low (e.g., 1 or 2 attempts) can lead to unnecessary lockouts.


Account Lockout Duration: Setting this too high can be inconvenient for users but increases security.


Reset Account Lockout Counter After: Setting this too short could allow attackers to repeatedly attempt to log in without triggering a lockout.



<ins>**Linking the GPO to an OU**<ins/>

Now that our GPO is configured, we need to add it to the appropriate OU where we want the policy to apply.

To do this we simply access the GPMC, right-click the OU or domain where you want to apply the GPO and select Link an Existing GPO. 
- In this sample, we will link the GPO to our EMPLOYEES OU so any user will have the same set of policies applied to them.

From the Link an Existing GPO screen, choose the GPO you created or modified earlier and click OK.

Once youve done this, your EMPLOYEES OU should have the GPO applied to it. Also remember to right click, and press "Enforce" or else your GPO wont be put into place. 

<img src="https://github.com/user-attachments/assets/d2086550-116b-4622-b887-daba17c8317d" >

<ins>**Updating Group Policy**<ins/>

Now that we have configured, added and linked our GPO to our OU, we need to update the group policy to ensure its being enforced. Normally, this is done automatically, but if you'd like to force an update you can open powershell as an administrator, and run the following command:

    gpupdate /force

This forces the computer and user policy to update within our domain, instead of waiting for it to be done manually. 

![image](https://github.com/user-attachments/assets/11bff098-3aaf-44d0-be59-6a2db7e16456)



