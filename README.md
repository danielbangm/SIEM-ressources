<p align="center">
<img src="https://shorturl.at/kBILY" />
</p>

<h1>SIEM: Azure Sentinel - Prerequisites and Installation</h1>

I will setup Azure Sentinel (SIEM) and connect it to a live virtual machine acting as a honey pot. We will observe live attacks (RDP Brute Force) from all around the world. We will use a custom PowerShell script to look up the attackers Geolocation information and plot it on the Azure Sentinel Map! 

<h2>Objectives</h2>

-  More Experience with Azure (I will Create the environment here)
-  Understanding the creation of VM, log analytic workspace, and Sentinel Azure.
-  Gain a better understanding of all parts of Active Directory such resetting passwords and setting up users.

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Virtual Machine(Honeypot-vm)
- log analytical workspaces(Lawhoneypot1)
- Azure Sentinel
- Remote Desktop

<h2>Operating Systems Used</h2>

-  Windows 10 pro

<h2>List of Prerequisites</h2>

-  All you need for this lab is the free Azure Tenant and Subscription

<h2>Installation steps</h2>

-  Step 1: Setup Ressource group, VM and Network Security Group in Azure

I am going to wwww.portal.azure.com and create a Virtual Machine(Honeypot-vm) with windows 10 installed in it with firewall(Network Security Group) set to be open to anything on the internet. The goal here is to make our VM most as vulnerable as possible to be discover by anyone on the internet.
![image](https://github.com/danielbangm/SIEM-ressources/assets/22795502/5af7cf61-58b6-4e5f-892c-d1b09dd2d9a2)
![image](https://github.com/danielbangm/SIEM-ressources/assets/22795502/ab5c4749-4849-4aed-be3c-b9ae132cbaaa)

-  Step 2: Set up Log Analytics workspaces

The purpose of this is to ingest logs from the Virtual Machine. We are going to ingest the Windows event logs and create our own custom logs that contains geographic information in order to discover where the attacker is coming from. To do that, just search for Log analytic workspaces on the portal and create one using the same ressource group. Then go on to Security center(Microsoft Defender for the Cloud) to enable the ability to gather logs from the virtual machine into the log analytic workspaces. Make sure to choose the log Analytics workspaces we just created and turn defender on and also data collection has to be set to "all". Finally go back to log Analytic workspaces and connect to the VM.
![image](https://github.com/danielbangm/SIEM-ressources/assets/22795502/b5ca8d9e-57b8-4be7-87bb-03140eb1a75c)

-  Step 3: Set up sentinel

We are going to use this as our SIEM to visualize the attack data. Just type azure sentinel in the search bar and create a new sentinel. Pick the log analytic workspaces we want to connect to oour logs.
![image](https://github.com/danielbangm/SIEM-ressources/assets/22795502/a4ed62a2-fa02-439a-a4df-b40116ebbec9)

-  Step 4: Connect to VM using Remote Desk Connection

Click on virtual machine in portal.azure and copy the public IP of the VM. Go on your desktop and launch remote desk Connection(Microsoft RDP) using the VM's public ip address , username and password we created earlier. and we have access to our virtual machine...
![image](https://github.com/danielbangm/SIEM-ressources/assets/22795502/e5fa5235-7e14-47f2-ae48-4a287af9e126)


