# Home SOC Lab with Microsoft Sentinel for SIEM &amp; Threat Detection
<img width="1339" height="884" alt="Image" src="https://github.com/user-attachments/assets/e0cd1ed1-fec4-481a-ad7f-15422821daa1" />

## Introduction

Proud to share my first project! I built a honeynet in Azure to simulate cyberattacks and learn how attackers operate. Along the way, I gained practical knowledge in Azure security, incident response, and hardening environments.


## Objective
My project involved deploying a single intentionally vulnerable virtual machine in Azure to observe real cyber attacks. This gave me practical experience with attacker techniques and improved my ability to respond quickly when security issues arose.

## Technologies, Regulations, and Azure Components used:

- Azure Virtual Network (VNet)
- Microsoft Sentinel for Security Information and Event Management (SIEM)
- Virtual Machine (Windows)
- Log Analytics Workspace with Kusto Query Language (KQL)
- Windows Remote Desktop Connection
- Azure Network Security Group (NSG)
- Azure Storage Account for Data Storage

## Components I used in my SOC Lab:

-	Begin by accessing Microsoft Azure and creating a free Azure subscription. This provides you with the essential cloud resources required for building and experimenting in your SOC Lab environment.

- To attract malicious attackers, you will need to set up a Honey Pot with Azure Virtual Machine which will be a Windows 10/11 VM exposed to the internet, attracting attackers.

- Once the Virtual Machine has been successfully created, verify its functionality by simulating failed login attempts, collecting security event logs, and analysing unauthorised logon attempts using Event Viewer.

-	To conduct a comprehensive analysis of logon attempts, security logs should be forwarded to a Log Analytics Workspace, where KQL (Kusto Query Language) can be utilised for detailed examination.

-	To identify the sources of all attacks, geolocation can be integrated into Microsoft Sentinel to provide information about attackers' IP addresses.

-	In order to provide insights to global threat sources, you would need to use Sentinel Workbook to visualise attackers’ activities on a map.


## Creating the Virtual Machine (Honeypot)
<img width="512" height="400" alt="Image" src="https://github.com/user-attachments/assets/b047aa85-362e-46dc-8e6e-1467e4f7cf49" />

In cybersecurity, a honeypot refers to a decoy system or network that is implemented to engage and observe attackers. Its purpose is to divert attention from actual systems and collect information about attack techniques and tools.

## Step 1: Create a resource group

Begin by navigating to https://portal.azure.com/ . In the search bar, enter "Resource Group" to locate the relevant section.

<br />
<img width="2468" height="411" alt="Image" src="https://github.com/user-attachments/assets/33c21b37-c36b-411a-ad6c-1bac82fd4141" />


 <br />
 <br />
 
Once you have selected a resource group, you will have the option to choose Create. After doing so, select your subscription, which should be Azure Subscription 1. The resource group name can be defined as you prefer, for example, I named mine CJ-SOC-LAB. Finally, choose the region where your resources will be deployed. For my setup, I selected North Europe. In this configuration, the resource group serves as a logical container, and the geographic location determines the region for the cloud SOC lab.

## Step 2: Create a Virtual Network

The virtual network forms the core infrastructure of your SOC lab, enabling secure communication between Azure resources such as virtual machines and log collection tools. Setting it up is essential as it ensures these components can interact and share data, which is critical for monitoring and analysing security events.

First head over to your Azure search bar, and type Virtual Network, you will then be prompted to create a virtual network. 

<br />
<img width="1369" height="305" alt="Image" src="https://github.com/user-attachments/assets/4170d01b-c8b4-4529-b5cf-b4bddca8ef15" />


 <br />
 <br />

Once that’s done, you will need to enter the following details:

<br />
<img width="1747" height="1297" alt="Image" src="https://github.com/user-attachments/assets/e424fadb-1901-450b-aa21-4a6740702f06" />


 <br />
 <br />

-	Resource Group: Select the existing group that you created from your side, I created CJ-SOC-LAB.
-	Region: Same region you selected previously, to keep you aligned with your resource group location, in this instance my region is North Europe.
-	Name of your VN: Keep it simple, I named mine VNET-SOC-LAB.

## Step 3: Create a Virtual Machine

In alignment with the previous steps, navigate to the Azure search bar and enter Virtual Machine. Once you arrive at the page, click on the create button, which will guide you through the process of setting up your Virtual Machine.

<br />
<img width="2260" height="799" alt="Image" src="https://github.com/user-attachments/assets/1025b393-754f-4465-b856-afc6bedabcd8" />

<br />
<br />

Use the same Resource Group, Azure subscription 1, and Region as before. For the Virtual Machine name, choose a realistic corporate-sounding option to attract brute force attempts.

<br />
<img width="1694" height="1035" alt="Image" src="https://github.com/user-attachments/assets/9354d0e4-a8f1-4810-9c43-cb456e6b8169" />

<br />
<br />

You will then be prompted to choose your base operating system for your VM, in which can be Windows 11 Pro, version 24H2 – x64 Gen2. As for the size this entirely depends on the amount of workload you want to run, the size that you choose will determines factors such as processing power, memory, and storage capacity. 
