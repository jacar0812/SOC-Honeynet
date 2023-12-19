# Building a SOC + Honeynet in Azure (Live Traffic)
![image](https://github.com/jacar0812/Cloud-Honeynet/assets/129025552/34353cc1-dd3d-4725-bb53-45095447dfda)

## Introduction

In this project, I spearheaded the comprehensive monitoring and proactive remediation efforts aimed at addressing the security vulnerabilities and potential threats identified in the prior initiative
Leveraging Microsoft Sentinel, these logs enable the creation of attack maps, alert triggers, and incident reports.
I conducted a security metric analysis in an unsecured setting for 24 hours, implemented security measures to strengthen the environment, conducted another 24-hour metric analysis, and presented the resulting improvements below

The metrics I will show are:

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture Before Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/aBDwnKb.jpg)

## Architecture After Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/YQNa9Pp.jpg)

The architecture of the mini honeynet in Azure consists of the following components:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 windows, 1 Linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

For the "BEFORE" metrics, all resources were deployed, and exposed to the internet. The Virtual Machines had both their Network Security Groups and built-in firewalls wide open, and all other resources were deployed with public endpoints visible to the Internet; aka, no use for Private Endpoints.

For the "AFTER" metrics, Network Security Groups were hardened by blocking ALL traffic except for my admin workstation, and all other resources were protected by their built-in firewalls as well as Private Endpoint

## Attack Maps Before Hardening / Security Controls
![NSG Allowed Inbound Malicious Flows](https://github.com/jacar0812/SOC-Honeynet/assets/129025552/c1168e9d-22f8-4dad-a8f2-ecea686197f6)<br>
![Linux Syslog Auth Failures](https://github.com/jacar0812/SOC-Honeynet/assets/129025552/14e62985-696d-4c39-9507-096a5468b41e)<br>
![Windows RDP/SMB Auth Failures](https://github.com/jacar0812/SOC-Honeynet/assets/129025552/dde0057f-8a9f-4170-b5a7-d6327ee8032a)<br>

## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:

**Start Time** 2023-11-30 19:54
**Stop Time** 2023-12-01 19:54

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 6741
| Syslog                   | 5154
| SecurityAlert            | 5
| SecurityIncident         | 129
| AzureNetworkAnalytics_CL | 2921

## Attack Maps Before Hardening / Security Controls

```All map queries returned no results due to no instances of malicious activity for the 24 hours after hardening.```

## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we applied security controls:

**Start Time** 2023-12-02 18:37
**Stop Time**	2023-12/03 18:37

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 3431
| Syslog                   | 10
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0


## RESULTS - After Securing the Environment 	

![image](https://github.com/jacar0812/SOC-Honeynet/assets/129025552/50763a94-a0b9-4133-8f30-f3070598fc8c)






## Conclusion

In this project, a mini honeynet was constructed in Microsoft Azure, and log sources were integrated into a Log Analytics workspace. Microsoft Sentinel was employed to trigger alerts and create incidents based on the ingested logs. Additionally, metrics were measured in the insecure environment before security controls were applied, and then again after implementing security measures. It is noteworthy that the number of security events and incidents was drastically reduced after the security controls were applied, demonstrating their effectiveness.

It is worth noting that if the resources within the network were heavily utilized by regular users, it is likely that more security events and alerts may have been generated within the 24-hour period following the implementation of the security controls.
