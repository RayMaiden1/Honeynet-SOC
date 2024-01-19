# <div align="center"> SOC and Honeynet in Azure with Live Traffic </div>
<div align="center"> <img width="900" alt="image" src="https://github.com/RayMaiden1/Honeynet-SOC/assets/101219588/e6848e8d-16b0-4db0-bb02-9ee143e852e5"> </div>

## Introduction

In the scope of this project, I created a mini honeynet in Azure and incorporated log sources from various resources into a Log Analytics workspace. The utilization of this data by Microsoft Sentinel facilitated the construction of intricate attack maps, the initiation of alerts, and the systematic tracking of incidents.

Following an initial 24-hour monitoring period for security metrics within an unsecured environment, strategic security controls were implemented to secure the infrastructure. Subsequently, an additional 24-hour measurement of metrics was conducted, with the ensuing results presented below. The metrics I will show are:

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture Before and After Hardening / Security Controls

The architecture of the mini honeynet in Azure consists of the following components:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 windows, 1 linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

In the initial assessment ("BEFORE" metrics), all resources were initially deployed and exposed to the internet. The Virtual Machines had open Network Security Groups and open built-in firewalls, and all other resources were deployed with visible public endpoints to the Internet, meaning no use for Private Endpoints.

In the subsequent evaluation ("AFTER" metrics), Network Security Groups were strengthened by blocking ALL traffic except for my admin workstation. Additionally, all other resources were safeguarded by both their built-in firewalls and Private Endpoints.

## Attack Maps Before Hardening / Security Controls

**Before NSG Malicious Allow-In** <br>
<img width="650" alt="image" src="https://github.com/RayMaiden1/Honeynet-SOC/assets/101219588/e718a4ab-d46d-420d-a241-892fd304cd7a"> <br>
**Before Linux SSH** <br>
<img width="650" alt="image" src="https://github.com/RayMaiden1/Honeynet-SOC/assets/101219588/7d61242c-deb0-400d-b655-5dec8239e10b"> <br>
**Before Windows RDP** <br>
<img width="650" alt="image" src="https://github.com/RayMaiden1/Honeynet-SOC/assets/101219588/058b75bf-943d-4a3e-a553-db534e1a899a">

## Metrics Before Hardening / Security Controls

The following table shows the metrics I measured in my insecure environment for 24 hours:

Start Time 2024-01-15 18:37:54

Stop Time 2024-01-16 18:37:54

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 34953
| Syslog                   | 2040
| SecurityAlert            | 3
| SecurityIncident         | 107
| AzureNetworkAnalytics_CL | 3817

## Attack Maps After Hardening / Security Controls

```All map queries returned no results due to no instances of malicious activity for the 24 hour period after hardening.```

## Metrics After Hardening / Security Controls

The following table shows the metrics I measured in my environment for another 24 hours after I have applied security controls:

Start Time 2024-01-17 11:18:55

Stop Time	2024-01-18 11:18:55

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 20797
| Syslog                   | 5
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion

In the course of this project, a mini honeynet was established in Microsoft Azure, with log sources logically integrated into a Log Analytics workspace. Microsoft Sentinel was utilized to activate alerts and manage incidents based on the ingested logs. Furthermore, I measured metrics in the initially vulnerable environment before and after the implementation of security controls. It's crucial to highlight that the application of security measures led to a significant reduction in the number of security events and incidents, underscoring their effectiveness. 

It's worth mentioning that if the network resources were extensively used by regular users, there could potentially have been more security events and alerts generated within the 24-hour period following the implementation of the security controls.
