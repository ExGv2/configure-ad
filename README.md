<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Computer)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>Deployment and Configuration Steps</h2>

![image](https://github.com/user-attachments/assets/2841b9f1-2970-4c0a-8f5d-a56372d3eab6)
Step 1: Create your "Resource Group" (Name it whatever you like, select region on US EAST 2)

![image](https://github.com/user-attachments/assets/b4a609e0-a7c3-4bf7-b625-8bbcd268d1fc)
Step 2: Create a "Virtual Network", assign it under your just created resource group, "review + create" (Make sure it is in the SAME region as your resource group)

![image](https://github.com/user-attachments/assets/e5121d66-907b-4490-aecc-26965d6ea99b)
Step 3: Create a virtual machine, assign it to the resource group you created in the beginning, Name it whatever you like (Again, make sure your region is also the SAME before creating the VM) 

![image](https://github.com/user-attachments/assets/ecb1d224-a0ad-491f-83c5-85f6f2bb8ab8)
Step 4: Make sure for the image to select "Windows Server 2022 Datacenter", then create your own username and password (Please take note of it before proceeding)

![image](https://github.com/user-attachments/assets/d0cc10ef-0001-4632-b2ef-11a383c8886f)
Step 5: Check licensing and confirmation

![image](https://github.com/user-attachments/assets/588ac30d-720a-4398-9bda-0d78c3378ec0)
Step 6: Proceed to "Review + Create"

![image](https://github.com/user-attachments/assets/f64c1667-f03f-4b79-88d5-c5574e74689a)
Step 7: Create a second VM, name VM to whatever you like, assign same resource group, SAME region as well

![image](https://github.com/user-attachments/assets/b23969e2-df93-465d-8756-744b4b46bca5)
Step 8: For the image select "Windows 10 Pro", create your own username and password (again, make sure to take note of it before proceeding)

![image](https://github.com/user-attachments/assets/207837e7-80f7-4e6a-a8dc-08a0750d8d6c)
Step 9: Confirm licensing

![image](https://github.com/user-attachments/assets/c1d99c3c-ae00-4efa-bd09-495691774d0c)
Step 10: Review + Create VM

![image](https://github.com/user-attachments/assets/c66a1958-9d3f-4535-b1f9-a1f132164501)
Step 11: Once both Virtual network and VMs have been created, we will proceed to assign the private IP addresses to STATIC (as shown in this image), this will make sure both the VMs are communicating exclusively to one another

![image](https://github.com/user-attachments/assets/7b5b2d44-1db2-437b-bf83-14da1b18f6cf)
Step 12: Go to Virtual Machines, select your DATACENTER VM, under "Networking", then "Network settings" you will find your private IP address (in this example, mine is 10.0.0.4)

![image](https://github.com/user-attachments/assets/a707f2c3-f950-4b46-b0b9-04451f72c092)
Step 13: Select Network Interface/IP configuration

![image](https://github.com/user-attachments/assets/6402273e-fcb5-4178-b081-5f0c98bc63c8)
Step 14: Select "ipconfig1", then select under "Allocation" select "static"

SIDE NOTE: For this tutorial, we will log into the DATACENTER VM to turn OFF all firewalls (This is for demonstration purposes only and is NOT recommended to do in a live environment)

![image](https://github.com/user-attachments/assets/70f77a73-acb4-43fc-9077-e94a526c707b)
Step 15: Under Virtual Machines locate your public IP address (In this example mine is 172.206.5.122)

![image](https://github.com/user-attachments/assets/b5cf0447-9fc5-494b-89b4-3e56265b8d6c)
Step 16: Open "Remote Desktop Connection" on your Windows PC, paste your public IP address

![image](https://github.com/user-attachments/assets/85567ea3-1330-4fad-9d78-9f24bcab13c6)
Step 17: Log in using the credentials you created for the virtual machine

![image](https://github.com/user-attachments/assets/5c5a3398-ebc5-48f8-bbe5-e746eee179c4)
Step 18: You should be in logged into the Server Manager VM (as shown)

![image](https://github.com/user-attachments/assets/306a656d-d1de-4af2-80c0-f1f42b5abd12)
Step 19: Under the taskbar search "Run" then type "wf.msc"

![image](https://github.com/user-attachments/assets/8ae51527-ea32-4593-9c73-1a4960548826)
Step 20: Select "Windows Defender Firewall Properties", then under the tabs "Domain Profile", "Private Profile is Active", and "Public Profile", TURN OFF firewall, then select "OK"

![image](https://github.com/user-attachments/assets/ed407845-c62d-45b2-a0c1-f064cf001b71)
Step 21: Going back to our VMs in Azure, we will now go to our HOST VM to change the DNS address

![image](https://github.com/user-attachments/assets/96322296-ab4a-4a1d-8894-546eda8ca949)
Step 22: Under the "Network interface/IP configuration", under "settings", select "DNS Servers", select "Custom" and type your DATACENTER PRIVATE IP address (for this example mine is 10.0.04)

![image](https://github.com/user-attachments/assets/9d8b7e03-a1df-43c1-832c-0de5d9a01817)
Step 23: To confirm both VMs have been correctly assigned, we will now log in to the HOST VM to confirm. Make sure you copy your public IP address to log in (mine is 172.200.214.33)

![image](https://github.com/user-attachments/assets/549c904a-d80c-4758-bf38-dd4d6b85b94b)
Step 24: Log into "Remote Desktop Connection" with the credentials you created for the VM.

![image](https://github.com/user-attachments/assets/75056000-6f96-4dab-805b-90cb448d9be9)
Step 25: Once in the HOST PC VMm, run "PowerShell" 

![image](https://github.com/user-attachments/assets/06885cbb-ac99-4449-a9c3-3ad257df0180)
Step 26: Type "ping" then YOUR private IP address, If successful you should receive a ping request as shown above.

This concludes the Virtual Machine tutorial

<h2>Installing Active Directory</h2>

![image](https://github.com/user-attachments/assets/c23851d8-9ab2-4976-9ccc-cd4767b5feba)
Step 1: Log into your DATACENTER VM on "Remote Desktop Connection"

![image](https://github.com/user-attachments/assets/a88db94b-301b-4dcc-acc7-f9d20d6cdb9f)
Step 2: Select "Add roles and features", then "Role-based or feature-based installation"

![image](https://github.com/user-attachments/assets/ea57c9b0-eaec-40d7-beb3-f204be9e36b8)
Step 3: The server selection should be the one you have as your datacenter

![image](https://github.com/user-attachments/assets/fefac5e1-9d0a-416f-a7e1-d28d2c1ab706)
Step 4: Under "Server Roles", you will check the box for "Active Directory Domain Services", then select "next"

![image](https://github.com/user-attachments/assets/673a6276-e317-4428-903a-269a2a7c0ddf)
Step 5: Under "Confirmation", check "Restart destination server automatically if required", then select "install"

![image](https://github.com/user-attachments/assets/400fdc86-39ef-4010-acc6-cedf540d7220)
Step 6: On the top right banner, select "Promote this server to a domain controller"

![image](https://github.com/user-attachments/assets/ce76e869-bd25-4c67-a23c-6d7bdbae9f79)
Step 7: We will create a new "root" domain, for this example we will use mydomain.com

![image](https://github.com/user-attachments/assets/23eda5a6-2824-4383-92ec-23155f4f17fb)
Step 8: Although we might not need it, create a password for the "DSRM"

![image](https://github.com/user-attachments/assets/c0da67f9-352a-4f3b-92b7-eef9929dbb3c)
Step 9: UNCHECK "Create DNS delegation"

![image](https://github.com/user-attachments/assets/c5e1611c-5cad-4ff8-8bf1-3a9d70136cd8)
Step 10: Proceed to "Prerequisites Check", then select "install"

SIDE NOTE: We will now create a MOCK organization for demonstartion purposes
IMPORTANT!: You will now be required to sign back into the VM using username "mydomain.com\" then whatever your username is

![image](https://github.com/user-attachments/assets/77bf11be-d600-43ac-8f6d-446351d221ae)
Step 11: In the Windows Taskbar open "Active Directory Users and Computers"

![Screenshot 2025-02-02 221355](https://github.com/user-attachments/assets/9a0aad5b-a4b8-4fcd-9ccc-662b3f9860bf)
Step 12: Right-click "mydomain.com", then select "new", then "Organizational Unit"

![image](https://github.com/user-attachments/assets/18c9a584-fe2e-406c-b769-5564445c9e21)
Step 13: Then type "_EMPLOYEES" (don't forget to include the underscore!)

![image](https://github.com/user-attachments/assets/b6c7f1e0-b890-4638-b352-de50cad57f9e)
Step 14: We will do the same as before, but this time create another unit called "_ADMINS"

![Screenshot 2025-02-02 222157](https://github.com/user-attachments/assets/cc5e8baf-ff20-4911-a178-58f8cbe394d4)
Step 15: We will now create a user in the "_ADMINS" folder

![image](https://github.com/user-attachments/assets/b0354bbe-3520-49d8-b7eb-75addc473607)
Step 16: You can name the user to whatever you like

![image](https://github.com/user-attachments/assets/c86c7cca-8195-415c-b066-c965f814facf)
Step 17: Create the user password (please take note of it before proceeding), UNCHECK "User must change password at next logon" (this is for demonstartion purposes only), then select "next"

![image](https://github.com/user-attachments/assets/511a645e-458c-45e5-bdfa-0cace40251dc)
Step 18: We will now make our admin part of the scurity group, right-click user then "properties", select tab "Member of", then select "Add"

![image](https://github.com/user-attachments/assets/6af5a22d-8789-4b09-aeca-ff73df3342ca)
Step 19: select tab "Member of", then select "Add"

![image](https://github.com/user-attachments/assets/2f2fcbac-b9ed-4324-a9f5-a956ab04e332)
Step 20: Type "Domain Names", then select "Check Names", it should now group this user under Domain Admins list, then select "Ok" then "Ok again.

![image](https://github.com/user-attachments/assets/ff4b4a82-832a-4584-accc-e4ce87dede61)
Step 21: Log into the HOST VM with your credentials. In the Windows taskbar type "about" then select "Rename this PC (advanced)", next select "Change...". Under "Member Of", "Domain", type "Mydomain.com" then select "OK"

![image](https://github.com/user-attachments/assets/c36707de-0d28-49a1-8e10-e0dd5d874d6d)
Step 22:You should now be prompted to log into the admin account we recently created (mine is jane_admin)

![image](https://github.com/user-attachments/assets/5e6d440a-4d7b-43f4-9001-f789e48a8c6c)
Step 23: To confirm Our HOST VM has merged with the DATACENTER VM, log back into the DATACENTER VM. In the Windows taskbar type "Active Directory Users and Computers". Then select the "Computers" folder, you should see your HOST PC in the list as shown above. 

![image](https://github.com/user-attachments/assets/3a423536-b41b-4bb4-95ba-db9c831db0af)
Step 24: Log into the HOST PC as our recently created admin user account. in the Windows Taskbar search "about", then select "Remote Desktop".

![image](https://github.com/user-attachments/assets/0893a80f-f7d0-4107-a216-591f22b3d09b)
Step 25: Select "Select users that can remotely access this PC" then select "add", then type "Domain Users", click "Check Names", select "ok", then "ok" again.

![Screenshot 2025-02-02 234111](https://github.com/user-attachments/assets/7320c85d-65a5-415b-81c0-2a04ee816dc7)
Step 26: Go back to the DATACENTER VM, in the Windows taskbar type "PowerShell ISE", right-click and "Run as Administrator"

![image](https://github.com/user-attachments/assets/a519b117-726d-4bf0-883f-fbd0af972982)
Step 27: You will create new script and run this script, this will create a MOCK list of USERS in the Active Directory [here](https://github.com/ExGv2/configure-ad/blob/main/Active%20Directory%20Script)

![image](https://github.com/user-attachments/assets/42319b13-9b8a-4b8a-acb9-0ecea0c8caba)
Step 28: It will now generate thousands of users.

