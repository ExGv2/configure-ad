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



