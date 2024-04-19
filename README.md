<p align="center">
<img src="https://shorturl.at/kBILY" />
</p>

<h1>SIEM: Microsoft Sentinel - Prerequisites and Installation</h1>

In this tutorial I will outline the prerequisites and installation of our virtual machine(Honeypot-vm) and configure our firewall to be open to everyone on the internet. We will create out log analytics workspaces

<h2>Objectives</h2>

-  More Experience with Azure (I will Create the environment here)
-  Understanding of the Domain Controler and DNS
-  Gain a better understanding of all parts of Active Directory such resetting passwords and setting up users.

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Virtual Machine(DC-1)
- Virtual Machine(client-1)
- Remote Desktop

<h2>Operating Systems Used</h2>

-  Windows Server 2022
-  Windows 10 pro

<h2>List of Prerequisites</h2>

-  All you need for this lab is the free Azure Tenant and Subscription

<h2>Installation steps</h2>

-  Step 1: Setup Ressource group, VM and Network Security Group in Azure

I am going to wwww.portal.azure.com and create a Virtual Machine(Honeypot-vm) with windows 10 installed in it with firewall(Network Security Group) set to be open to anything on the internet. The goal here is to make our VM most as vulnerable as possible to be discover by anyone on the internet.
![image](https://github.com/danielbangm/SIEM-ressources/assets/22795502/5af7cf61-58b6-4e5f-892c-d1b09dd2d9a2)
![image](https://github.com/danielbangm/SIEM-ressources/assets/22795502/ab5c4749-4849-4aed-be3c-b9ae132cbaaa)

-  Step 2: Set up Log Analytics workspaces

The purpose of this is to ingest logs from the Virtual Machine. We are going to ingest the Windows event logs and create our own custom logs that contains geographic information in order to discover where the attacker is coming from. To do that, just search for Log analytic workspaces on the portal and create one using the same ressource group. Then go on to Security center(Microsoft Defender for the Cloud) to enable the ability to gather logs from the virtual machine into the log analytic workspaces. Make sure to choose the log Analytics workspaces we just created and turn defender on and also data collection has to be set to "all"
![image](https://github.com/danielbangm/configure-ad/assets/22795502/2459439d-9850-4d35-acb5-5905ecbc3482)

-  Step 3: Ensure Connectivity between the client and Domain Controller

I connect to client-1 Virtual Machine through Remote Desk Connection and I will try to ping DC-1's address with a perpetual(-t) ping to see if there is a connection established. I see that the ping -t 10.0.0.4 is timeout probably because DC-1 Firewall is blocking ICMPv4 traffic
![image](https://github.com/danielbangm/configure-ad/assets/22795502/ed15f1ee-52a4-4fa3-9252-61e6c882e090)

To solve this issue, I am going to log into DC-1 through Remote Desktop Connection using DC-1 Public IP address and enable ICMPv4 in the local Windows Firewall. Go to Windows Defender Firewall with advanced security -> Inbound Rules -> Protocol -> ICMPv4 -> Enable Rules.
![image](https://github.com/danielbangm/configure-ad/assets/22795502/676ced27-4310-4f7b-b5f4-edbe460c3034)

Now I going back to client-1 and notice that the ping -t 10.0.0.4 starts working after I enabled the firewall rules in DC-1
![image](https://github.com/danielbangm/configure-ad/assets/22795502/039b13a5-9efa-4dbc-b5d5-d5923128c1ed)

-  Step 4: Install Active Directory

I log in to DC-1 and install Active Directory. Go to Server Manager -> Add Roles and Features -> Active Directory Domain Services -> Install
![image](https://github.com/danielbangm/configure-ad/assets/22795502/cd87f549-b47c-43cb-9f26-df57d6c3fe81)

Now I am going to promote this server as a Domain Controller and Setup a new forest as daniel.com. To do so I just click on the upper right conner of the previous snippet on that yellow triangle. When everything is done it automatically logs me out. Because DC-1 is now a Domain Controller, in order to log in I have to use a different username which is <b>daniel.com\labuser</b>

