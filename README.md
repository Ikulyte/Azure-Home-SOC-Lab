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

<br />
<img width="1125" height="742" alt="Image" src="https://github.com/user-attachments/assets/37c406fe-479b-46ab-bc36-a2db026555f1" />

<br />
<br />

This field will be the administrator credential for your VM and your password. For your inbound ports, RDP (3389) will allow traffic from the public internet to one of these common ports.

<br />
<img width="1139" height="518" alt="Image" src="https://github.com/user-attachments/assets/06ed738b-066f-4053-bd82-d7e42c88342e" />

<br />
<br />

Once you have completed all necessary configuration steps for your virtual machine, proceed by selecting next to review each tab. Retain the default settings unless you require specific adjustments for your virtual machine. After carefully reviewing all the tabs, click on review + create, to finalise your VM. If the validation passes, select the button create to deploy your virtual machine which will be ready to go.

Your final result should look like this:

<br />
<img width="2186" height="1304" alt="Image" src="https://github.com/user-attachments/assets/b1e24a09-9b44-4c88-a0b7-544b7b8a4a6a" />

<br />
<br />

Once you have successfully deployed your virtual machine, you can logon to it by using the Remote Desktop Connection (RDC) on your Windows PC.

## Step 4: Access your Virtual Machine via RDC

To access your Virtual Machine, go through your Azure Portal then select the VM you recently created. Inside your VM dashboard, you will notice there is a Public IP Address, copy that IP address. 

Once that’s done, on your actual Windows PC, open Remote Desktop Connection (RDC) application.  Paste your Public IP Address you copied. It will then prompt you to add your Username and Password you configured during the creation of your Virtual Machine.

<br />
<img width="789" height="452" alt="Image" src="https://github.com/user-attachments/assets/cba913ea-c13c-4d1e-a7f8-33c314a1fd0f" />

<br />
<br />

Once you successfully accessed your Virtual Machine, you will be able to proceed with any changes within your VM to complete the setup of your SOC Lab.

<br />
<img width="1120" height="701" alt="Image" src="https://github.com/user-attachments/assets/e4aa5b16-5024-4186-b294-a9abf18f5739" />

<br />
<br />

Once you have access to your Virtual Machine, locate the Firewall application within your VM. Proceed to disable the Domain Profile, Private Profile, and Public Profile. This action will enable you to observe potential attempts by unauthorised users to access your VM.

<br />
<img width="734" height="645" alt="Image" src="https://github.com/user-attachments/assets/cc0e05c4-d457-4070-92d4-6e6c2a9a61e0" />

<br />
<br />

## Step 5 : Security Events Testing

To test your VM and security events, shut down your VM, then try logging in from the RDC (Remote Desktop Connection) with random usernames and passwords several times to generate failed attempts for review in Event Viewer.

<br />
<img width="1101" height="202" alt="image" src="https://github.com/user-attachments/assets/1db78bea-f706-4c36-869a-fe2890e34983" />

<br />
<br />

To view failed login attempts access your VM, search for Event Viewer in Windows, open it, and go to Windows Logs > Security. Use "Filter Current Log" on the right, enter Event ID 4625, and you'll see records of failed logins, indicating possible unauthorised access attempts to your VM.

Next, you will want to see those logs inside Microsoft Sentinel, to do so, head toward your Azure Portal and search Microsoft Sentinel. Open the Log Analytics Workspace associated with your lab, find Content Management then select Content Hub. You will then search for Windows Security Events and install it.

<br />
<img width="2252" height="1097" alt="Image" src="https://github.com/user-attachments/assets/17c982e2-2afb-406b-ab63-3c6737cae600" />

<br />
<br />

After installation, select Manage to proceed to the next page, then choose Windows Security Events via AMA. On the right side, you will find the option to "Open connector page to configure the data ingestion." You will then be prompted to create a new Data Collection Rule (DCR). Complete the three required fields: Rule Name (e.g., DCR-Windows), Subscription (such as Azure subscription 1), and Resource Group (your designated resource group). Once these fields are filled, the configuration will be complete.

## Step 6: Use of KQL to view the failed login attempts

To use KQL (Kusto Query Language), go to Log Analytics Workspace and select Logs. You can run queries like SecurityEvents to efficiently analyse large volumes of security event data collected from Virtual Machines.

<br />
<img width="2180" height="1308" alt="Image" src="https://github.com/user-attachments/assets/6dc1fda9-ba1a-4039-860e-4733a142d6f3" />

<br />
<br />

After conducting several tests of my KQL, I proceeded to analyse unsuccessful login attempts made by external parties on my VM.

<br />
<img width="1480" height="1058" alt="Image" src="https://github.com/user-attachments/assets/72fdbc82-7ae4-45c1-b3bd-cdb43ba77f88" />

<br />
<br />

## Step 7: Use of GeoIP Watchlist

The final step is to assign geographic locations to the source IP addresses involved in the activity. This process involves creating a Watchlist in Microsoft Sentinel and uploading a CSV file containing geolocation data such as IPs, countries, cities, and coordinates.

To create a Watchlist, navigate to Microsoft Sentinel, select Configuration, and locate the Watchlist option. Select New to initiate the creation of a watchlist, which can be named "geoip".

<br />
<img width="2001" height="1314" alt="Image" src="https://github.com/user-attachments/assets/8a0c5eb0-76c9-465c-b9c5-5e7a743683f1" />

<br />
<br />

Begin by uploading your data to the platform. To investigate failed login attempts, use a KQL query with relevant identifiers such as IP addresses or specific Event IDs (for example, 4625). When you run the query, it will provide details like IP address, timestamp, city, and country information. You can then use these results to conduct a geographic analysis of security incidents. The result will then allow you to locate where the attack comes from. 

<br />
<img width="1506" height="999" alt="Image" src="https://github.com/user-attachments/assets/4b423fb4-a1d5-47e7-b09a-fb865e729682" />

<br />
<br />

VirusTotal is a platform that allows users to investigate whether an IP address is associated with malicious activity. Personally, I use it to trace the origin of suspicious IPs, examine the nature of their malicious behaviour, and, when necessary, report them accordingly.

<b />
<img width="1114" height="582" alt="Image" src="https://github.com/user-attachments/assets/fc3f46c9-d77a-41cf-a498-9bbea711ff48" />

<b >/
<b >/

In the last 24 hours, I was able to locate a few attackers attempting to login inside my VM.

<b />
<img width="2010" height="1047" alt="Image" src="https://github.com/user-attachments/assets/7fcb6a25-39b3-47e0-b100-6db9e0209a5a" />

<b />
<b />

## Conclusion

To summarise, I deployed a lightweight yet efficient honeynet leveraging Microsoft Azure’s powerful cloud platform. Microsoft Sentinel was configured to generate alerts and incidents by analysing logs from the designated watch lists. Initial baseline metrics were collected in the unprotected environment prior to introducing any security measures. The next phase will involve implementing a range of security measures to strengthen the network and then collecting a second set of measurements for comparison.
