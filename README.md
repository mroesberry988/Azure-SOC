# Azure-SOC
# Building a SOC + Honeynet in Azure (Live Traffic)


## Introduction

In this project, I built a mini honeynet in Azure and ingested log sources from various resources into a Log Analytics workspace, which is then used by Microsoft Sentinel to build attack maps, trigger alerts, and create incidents. I measured some security metrics in the insecure environment for 24 hours, apply some security controls to harden the environment, measure metrics for another 24 hours, then show the results below. The metrics we will show are:

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture Before Hardening / Security Controls
ADD PICTURE

## Architecture After Hardening / Security Controls
ADD PICTURE


The architecture of the mini honeynet in Azure consists of the following components:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 windows, 1 linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

For the "BEFORE" metrics, all resources were originally deployed, exposed to the internet. The Virtual Machines had both their Network Security Groups and built-in firewalls wide open, and all other resources are deployed with public endpoints visible to the Internet; aka, no use for Private Endpoints.

For the "AFTER" metrics, Network Security Groups were hardened by blocking ALL traffic with the exception of my admin workstation, and all other resources were protected by their built-in firewalls as well as Private Endpoint


## Attack Maps Before Hardening / Security Controls

![image](https://github.com/mroesberry988/Azure-SOC/assets/134666751/d1870547-5ec6-4d3a-b359-2603860b1426)


![image](https://github.com/mroesberry988/Azure-SOC/assets/134666751/87a30b7d-0f0d-4e6c-a8e8-d4051b60df78)


![image](https://github.com/mroesberry988/Azure-SOC/assets/134666751/248ae4ce-8872-4feb-ab07-bae1f97dbedb)



## Metrics Before Hardening / Security Controls


The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time 2024-04-08 12:08:13
Stop Time  2024-04-09 12:08:13 

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 13885
| Syslog                   | 6104
| SecurityAlert            | 0
| SecurityIncident         | 214
| AzureNetworkAnalytics_CL | 2170


## Attack Maps Before Hardening / Security Controls

```All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.```

## Metrics After Hardening / Security Controls


The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
Start Time 2024-05-28 4:56:21
Stop Time	 2024-05-29 4:56:21

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 9180
| Syslog                   | 1
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0


## Conclusion

The following table shows the metrics of the difference in results of change after securing the environment. 

| Metric                   | Percentage 
| ------------------------ | -----
| SecurityEvent            | -33.89%
| Syslog                   | -99.98%
| SecurityAlert            |  0.00%
| SecurityIncident         | -100.00%
| AzureNetworkAnalytics_CL | -100.00%


In this project, a mini honeynet was constructed in Microsoft Azure and log sources were integrated into a Log Analytics workspace. Microsoft Sentinel was employed to trigger alerts and create incidents based on the ingested logs. Additionally, metrics were measured in the insecure environment before security controls were applied, and then again after implementing security measures. It is noteworthy that the number of security events and incidents were drastically reduced after the security controls were applied, demonstrating their effectiveness.

It is worth noting that if the resources within the network were heavily utilized by regular users, it is likely that more security events and alerts may have been generated within the 24-hour period following the implementation of the security controls.
