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

![Image](https://github.com/user-attachments/assets/ee42a391-0c7b-4b0f-888e-b09f9d9bf72e)

![Image](https://github.com/user-attachments/assets/5a67e40c-0ea7-47c0-ad43-3b196d2472b5)

![Image](https://github.com/user-attachments/assets/82e186fd-85ab-466e-9ec7-6a653177ce96)

![Image](https://github.com/user-attachments/assets/b1cd2a1a-b813-48d8-b27e-1022db611e36)

![Image](https://github.com/user-attachments/assets/915b944e-2e18-4c6b-a89e-573063524e0d)

![Image](https://github.com/user-attachments/assets/c752ea4f-8c4b-4784-8b2b-d55cb4862445)

![Image](https://github.com/user-attachments/assets/d4fc2e31-c603-4b92-8880-3df57290359c)

Now we are gonna test the Account Lockout Policy. Use any non-admin account and attempt to login more than 5 times with a wrong password, after the 5th attempt you should get a notification saying that your account has been locked and you need to contact your system administrator. Now we are gonna log into out Admin account to fix the account lockout. Using your Admin account open Active Directory Users and Computers, go to the OU where the currently locked account is (in my case the _EMPLOYEES OU) right click on the folder, and click Find. Type the name of the account on the Name search bar, click Find Now and you should see the account we are looking for in the Search results. Right-click the account to check the properties, on the account tab you can see that the account is currently locked and you can check the box to unlock it, do that and then go to Account options and click "User must change password at next logon" then click OK.

![Image](https://github.com/user-attachments/assets/b2fe6d35-b7f6-4481-9b7c-e6747c6d62e3)

![Image](https://github.com/user-attachments/assets/68d30359-8cbc-4975-9ed6-13590355fc06)

![Image](https://github.com/user-attachments/assets/dfb7cb62-86a3-42aa-8abe-df170a633faf)

![Image](https://github.com/user-attachments/assets/c51762f2-5452-4638-ad89-2df8c7961a14)

![Image](https://github.com/user-attachments/assets/37586042-b777-4f35-bd98-2893bba0efb0)

Let's say our user forgot their password but we don't have to unlock the account. We can find the account again (either by going to the right OU or by using the Find option) then right-click the account and click Reset Password. Here you can create a new password for the user and also check User must change password at next logon so they can choose their new password. If an account has been compromised or is no longer in use but you don't want to delete it you can also go to the account, right-click it and click Disable Account. This will make it impossible for anyone to use the account until you Enable it again. 

![Image](https://github.com/user-attachments/assets/bad944b6-2570-4ab1-a5e4-fd59f77f3575)

![Image](https://github.com/user-attachments/assets/0bf9fed8-65b8-4091-bcef-6398531a4d90)

![Image](https://github.com/user-attachments/assets/2e2eab6e-ecfb-4afa-8af0-cc066a4a22c2)

You can also monitor the logins across all the computers and users going through our domain. We do this using the Event Viewer tool which you can open through the "Run" program by typing **eventvwr.msc**.
On the left side, you can open the drop-down menu for Windows log, right-click on Security and click Find. Here you can look for a specific user and monitor all the login history. You can also use **cntrl+f** and look for specific events using Event IDs. Some of the most common Event IDs that you can look for are **4625** for Failed logon, **4740** for User account locked out, **4726** for User account deleted.

![Image](https://github.com/user-attachments/assets/1f3e769e-9954-4de1-85ef-89a90d78488b)

![Image](https://github.com/user-attachments/assets/5e4c16f3-8817-499a-a0ad-ed7c4d178d6a)

![Image](https://github.com/user-attachments/assets/c94e9b19-cea0-41d5-8bb8-546a672bd9fa)

**Congratulations!** Now you can deploy your own Active Directory environment, manage accounts, monitor their activity, and change Group Policies for your users. 










