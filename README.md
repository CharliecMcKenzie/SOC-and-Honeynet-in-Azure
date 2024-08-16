# Building a SOC and Honeynet in Azure

## Project Description

In this project, I set up a mini honeynet in Azure and configured various resources to send log data into a Log Analytics workspace. Microsoft Sentinel uses this data to generate attack maps, trigger alerts, and create incidents. Initially, I monitored the insecure environment for 24 hours to gather baseline security metrics. Afterward, I applied security controls to harden the environment and conducted another 24-hour monitoring period to measure the impact of these controls. Below are the key metrics we will show:
- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents Created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows Allowed into the Honeynet)

## Project walk-through:

The architecture of the mini honeynet in Azure consists of the following components:
- Virtual Network (VNet) 
- Network Security Group (NSG) 
- Virtual Machines (2 windows, 1 linux) 
- Log Analytics Workspace 
- Azure Key Vault 
- Azure Storage Account 
- Microsoft Sentinel 

For the 'BEFORE' metrics, all resources were initially deployed and fully exposed to the internet. The Virtual Machines had unrestricted access through their Network Security Groups and built-in firewalls, while other resources were accessible via public endpoints, with no Private Endpoints in use.
For the 'AFTER' metrics, I applied security hardening measures by configuring the Network Security Groups to block all traffic except from my admin workstation. Additionally, all other resources were secured using built-in firewalls and Private Endpoints to limit external exposure.

### Before Hardening Security

<p align="center">
<img src="https://i.imgur.com/TOXzreT.png" height="80%" width="80%" alt="attackmaps"/>
<img src="https://i.imgur.com/6ueEq1o.png" height="80%" width="80%" alt="attackmaps"/>
<img src="https://i.imgur.com/vltItQO.png" height="80%" width="80%" alt="attackmaps"/>

After 24 hours, these are the results gathered from the insecure environment. 
| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 54800
| Syslog                   | 1561
| SecurityAlert            | 142
| SecurityIncident         | 24
| AzureNetworkAnalytics_CL | 1698

### After Hardening Security

Results after implementing security hardening measures for 24 hours.
| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 7800
| Syslog                   | 25
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Summary
In this project, a mini honeynet was created in Microsoft Azure, with log sources integrated into a Log Analytics workspace. Microsoft Sentinel was used to generate alerts and create incidents based on the ingested logs. Security metrics were measured in the insecure environment both before and after the application of security controls. The results clearly demonstrated the effectiveness of these measures, as the number of security events and incidents significantly decreased following the implementation of the controls. 
