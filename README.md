# Building a SOC + Honeynet in Azure (Live Traffic 24 Hour)
![image](https://github.com/user-attachments/assets/70e935e6-60eb-46a7-b1da-12b73d1c4109)

## Introduction

In this project, I leveraged my expertise to set up a mini honeynet in Azure, successfully integrating log sources from various resources into a Log Analytics workspace. I used Microsoft Sentinel to build attack maps, trigger alerts, and generate incidents. I conducted a 24-hour security assessment in an unsecured environment, applied targeted security controls to enhance the system, and then measured the improvements during another 24-hour assessment. The following metrics highlight the impact of my work.

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture Before Hardening / Security Controls
![image](https://github.com/user-attachments/assets/eafedfa5-b2a5-4b2a-b01a-2c965a3ca97e)


## Architecture After Hardening / Security Controls
![image](https://github.com/user-attachments/assets/9414d97b-81dc-4fa5-b353-7b9e1560d7ad)


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
![image](https://github.com/user-attachments/assets/2521f4cc-4991-4696-9b7c-0ee09478dd47)<br>
![image](https://github.com/user-attachments/assets/faf18229-6847-4ecb-88d1-5232de7e5e8a)<br>

## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time 2024-07-15 17:04:29
Stop Time 2024-07-16 17:04:29

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 4358
| Syslog                   | 2345
| SecurityAlert            | 6
| SecurityIncident         | 73
| AzureNetworkAnalytics_CL | 103

## Attack Maps Before Hardening / Security Controls

```All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.```

## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
Start Time 2024-07-18 15:37
Stop Time	2024-07-19 15:37

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 110
| Syslog                   | 344
| SecurityAlert            | 1
| SecurityIncident         | 2
| AzureNetworkAnalytics_CL | 0

## Conclusion

In this project, I designed and deployed a mini honeynet within Microsoft Azure, integrating log sources into a Log Analytics workspace. I utilized Microsoft Sentinel to trigger alerts and generate incidents based on the collected logs. To assess the effectiveness of security controls, I first measured key metrics in an unsecured environment, then re-evaluated after applying targeted security measures. The results clearly indicated a significant reduction in security events and incidents post-implementation, underscoring the effectiveness of the applied controls.

It's important to note that if the network resources were under heavy utilization by regular users during the 24-hour period after the controls were applied, it is likely that a higher number of security events and alerts might have been observed.
