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
