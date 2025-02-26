<p align="center">
  
![Image](https://github.com/user-attachments/assets/ad8da1a3-4fff-4af2-bd17-cdd14d39da67)


<h1>Group Policy and Account Managemet</h1>
This guide outlines the process for changing group policy within active directory, we will also learn how to lock and unlock accounts and monitor account activity <br />




<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines)
- Remote Desktop/Bastion
- Active Directory Users and Computers
- Group Policy Management
- Event Viewer

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Windows Server 2022 

<h2>High-Level Deployment and Configuration Steps</h2>

- Change Policy on account lockout
- Enforce Policy from Command Prompt
- Unlock account and reset passwords
- Check login attempts inside Event Viewer


  
<h2>Group Policy</h2>

We are gonna change a simple group policy within our Active Directory Environment, this allows us to change configurations and enforce security policies on multiple devices at the same time. For this example we are gonna change the Account Lockout Policy to change the ammount of failed login attemps required before an accounts locks out. I created a new user (without domain admin privileges) under the _EMPLOYEES OU named Morty Sanchez for this test. 

To access the Group Policy Management tool you can open the "Run" program and type **gpmc.msc**. Under the domain name you should see the Default Domain Policy, right click it and click Edit. You should see all the different folder that contain the different policies. Open the Policies folder then Open the following folders: Windows Settings>Security Settings>Account Lockout Policy. In the right side you can see all the different policies under the Account Lockout Policy that we can define. Click on Account Lockout Duration, here we can change how long the account will stay locked after enough failed login attempts. We will set it for 30 minutes and click OK. Now click on Allow Administrator account lockout and enable it then press OK. You can also change the Account Lockout Threshold to change how many failed attempts it takes to trigger the lockout, I set mine to 5 attempts. After changing the Policy you can click on Default Domain Policy and go to Settings on the right side and scroll down to Account Policies/Account Lockout Policy and check that the changes we made appear here. 

The changes we do to the Group Policy don't happen immediately, usually Active Directory updates the policy every 90 to 120 minutes, but there's a faster way to update the group policy. Open The Command Prompt and type the command **gpupdate /force**, this will immediately force an update. 




